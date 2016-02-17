---
layout: post
title:  "Instant converter"
categories: java
tags: java8
---

{% highlight java %}
import java.time.Instant;
import java.util.Date;
import javax.persistence.AttributeConverter;
import javax.persistence.Converter;

@Converter(autoApply = true)
public class InstantConverter implements AttributeConverter<Instant, Date> {

    @Override
    public Date convertToDatabaseColumn(Instant instant) {
        return instant == null ? null : Date.from(instant);
    }

    @Override
    public Instant convertToEntityAttribute(Date date) {
        return date == null ? null : date.toInstant();
    }
}
{% endhighlight %}

{% highlight java %}
import spock.lang.Specification

import java.time.Instant

class InstantConverterSpec extends Specification {

    InstantConverter converter = new InstantConverter();

    def 'should convert to database column'() {
        given:
            Instant instant = Instant.now()
        expect:
            converter.convertToDatabaseColumn(instant) == Date.from(instant)
    }

    def 'should convert to entity attribute'() {
        given:
            Date date = new Date()
        expect:
            converter.convertToEntityAttribute(date) == date.toInstant()
    }
}
{% endhighlight %}

