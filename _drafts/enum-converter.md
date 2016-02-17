---
layout: post
title:  "Enum converters in Java 8"
categories: java
tags: java8
---

{% highlight java %}
import javax.persistence.AttributeConverter;
import javax.persistence.Converter;

@Converter(autoApply = true)
public class EventTypeConverter implements AttributeConverter<EventType, Character> {

    @Override
    public Character convertToDatabaseColumn(EventType eventType) {
        return eventType.shortName();
    }

    @Override
    public EventType convertToEntityAttribute(Character shortName) {
        return EventType.fromShortName(shortName);
    }
}
{% endhighlight %}


{% highlight java %}
import spock.lang.Specification
import spock.lang.Unroll


class EventTypeConverterSpec extends Specification {
    EventTypeConverter converter = new EventTypeConverter();

    @Unroll
    def 'should convert event type #eventType to database column #expectedChar'() {
        expect:
            converter.convertToDatabaseColumn(eventType) == expectedChar
        where:
            eventType  || expectedChar
            REDIRECTED || 'R'
            CHARGED    || 'C'
            SETTLED    || 'S'


    }

    @Unroll
    def 'should convert database column #dbChar to event type #expectedType'() {
        expect:
            converter.convertToEntityAttribute(dbChar as char) == expectedType
        where:
            dbChar || expectedType
            'R'    || REDIRECTED
            'C'    || CHARGED
            'S'    || SETTLED
    }
}
{% endhighlight %}


{% highlight java %}
import java.util.Arrays;

public enum EventType {
    /**
     * Customer was redirected to payment window
     */
    REDIRECTED('R'),
    /**
     * Customer's card was charged, we received callback from payment provider
     */
    CHARGED('C'),
    /**
     * Charged payment was successfully sent to backoffice.
     */
    SETTLED('S');

    private final Character shortName;

    EventType(Character shortName) {
        this.shortName = shortName;
    }

    public Character shortName() {
        return shortName;

    }

    public static EventType fromShortName(Character shortName) {
        return Arrays.stream(values())
                .filter(e -> e.shortName().equals(shortName))
                .findFirst()
                .orElseThrow(() -> new IllegalArgumentException("Unknown short name: " + shortName));
    }
}
{% endhighlight %}
