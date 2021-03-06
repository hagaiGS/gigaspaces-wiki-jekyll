---
layout: post100
title:  Basic Index
categories: XAP100
parent: indexing-overview.html
weight: 50
---

{% summary %}{% endsummary %}

{%comment%}
{% summary %} Using indexes to improve query performance. {% endsummary %}

# Overview




When a space is looking for a match for a read or take operation, it iterates over non-null values in the template, looking for matches in the space. This process can be time consuming, especially when there are many potential matches. To improve performance, it is possible to index one or more properties. The space maintains additional data for indexed properties, which shortens the time required to determine a match, thus improving performance.

# Choosing which Properties to Index
{%endcomment%}


One might wonder why properties are not always indexed, or why all the properties in all the classes are not always indexed. The reason is that indexing has its downsides as well:

- An indexed property can speed up read/take operations, but might also slow down write/update operations.
- An indexed property consumes more resources, specifically memory footprint per entry.

# When to Use Indexing

Naturally the question arises of when to use indexing. Usually it is recommended to index properties that are used in common queries. However, in some scenarios one might favor less footprint, or faster performance for a specific query, and adding/removing an index should be considered.

{% warning %}  Remember that "Premature optimization is the root of all evil". It is always recommended to benchmark your code to get better results. {%endwarning%}

# Index Types

The index type is determined by the **`SpaceIndexType`** enumeration. The index types are:

**`NONE`** - No indexing is used.

**`BASIC`** - Basic index is used - this speeds up equality matches (equal to/not equal to).

**`EXTENDED`** - Extended index - this speeds up comparison matches (bigger than/less than).

# Indexing at Design-time

Specifying which properties of a class are indexed is done using annotations or gs.xml.

{% inittab %}
{% tabcontent Annotations %}

{% highlight java %}
@SpaceClass
public class Person
{
    private String lastName;
    private String firstName;
    private Integer age;

    ...
    @SpaceIndex(type=SpaceIndexType.BASIC)
    public String getFirstName() {return firstName;}
    public void setFirstName(String firstName) {this.firstName = firstName;}

    @SpaceIndex(type=SpaceIndexType.BASIC)
    public String getLastName() {return lastName;}
    public void setLastName(String name) {this.lastName = name;}

    @SpaceIndex(type=SpaceIndexType.EXTENDED)
    public Integer getAge() {return age;}
    public void setAge(Integer age) {this.age = age;}
}
{% endhighlight %}

{% endtabcontent %}
{% tabcontent XML %}

{% highlight java %}
<gigaspaces-mapping>
    <class name="com.gigaspaces.examples.Person" persist="false" replicate="false" fifo="false" >
        <property name="lastName">
            <index type="BASIC"/>
        </property>
        <property name="firstName">
            <index type="BASIC"/>
        </property>
        <property name="age">
             <index type="EXTENDED"/>
        </property>
    </class>
</gigaspaces-mapping>
{% endhighlight %}

{% endtabcontent %}
{% endinittab %}

## Inheritance

By default, a property's index is inherited in sub classes (i.e. if a property is indexed in a super class, it is also indexed in a sub class). If you need to change the index type of a property in a subclass you can override the property and annotate it with `@SpaceIndex` using the requested index type (to disable indexing use `NONE`).

# Indexing at Run-time

Indexes can be added dynamically at run-time using the GigaSpaces Management Center GUI or via API using the `GigaSpaceTypeManager` interface in conjunction with `SpaceIndexFactory`. See example below:

{% highlight java%}
   gigaspace.getTypeManager().asyncAddIndex("MyDataType",
   SpaceIndexFactory.createPropertyIndex("myProperty", SpaceIndexType.BASIC));
{%endhighlight%}


{% note %} Removing an index or changing an index type is currently not supported. {%endnote%}


# Performance Tips

Properties that are not indexed and not used for queries can be grouped within a user defined class (also known as payload class). This improves the read/write performance since these properties would not be introduced to the space class model.

# Deprecated Indexing Options

## Implicit Indexing

If no properties are indexed explicitly, the space implicitly indexes the first **n** properties (in alphabetical order), where **n** is determined by the `number-implicit-indexes` property in the space schema.

{% note %} Using this feature is not recommended, since adding/removing properties can have unexpected side effects. It is deprecated, and might be removed in future versions.{%endnote%}

# Query Execution Flow

When a read, take, readMultiple, or takeMultiple call is performed, a template is used to locate matching space objects. The template might have multiple field values - some might include values and some might not (i.e. `null` field values acting as wildcard). The fields that do not include values are ignored during the matching process. In addition, some class fields might be indexed and some might not be indexed.

When multiple class fields are indexed, the space looks for the field value index that includes the smallest amount of matching space objects with the corresponding template field value as the index key.

The smallest set of space objects is the list of objects to perform the matching against (matching candidates). Once the candidates space object list has been constructed, it is scanned to locate space objects that fully match the given template - i.e. all non-null template fields match the corresponding space object fields.

{% info%} Class fields that are not indexed are not used to construct the candidates list. {%endinfo%}



<ul class="pager">
  <li class="previous"><a href="./indexing-overview.html">&larr; Indexing Overview</a></li>
  <li class="next"><a href="./indexing-nested-properties.html">Indexing Nested Properties &rarr;</a></li>
</ul>
