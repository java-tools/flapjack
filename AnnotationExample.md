# Using annotations to map the fields to your domain model [SourceCode](http://github.com/born2snipe/flapjack/tree/master/flapjack-example/src/test/java/flapjack/example/UseAnnotationTest.java)

# Record Specification #

### User Record ###
| Name | Position | Length |
|:-----|:---------|:-------|
| Artist | 0 | 10 |
| Title | 10 | 10 |
| Length of Song | 20 | 5 |

So first we will have to define our record layout:
```
    private static class SongRecordLayout extends SimpleRecordLayout {
        private SongRecordLayout() {
            field("Artist", 10);
            field("Title", 10);
            field("Length of Song", 5);
        }
    }
```

We now need to define our domain model that will represent this record type. The `@Record` requires you to tell what `RecordLayout` is tied to this class. Also the `@Field` can be given the id of the field or if nothing is given it will attempt to match up the field in the data to a field on the model object.
```
@Record(SongRecordLayout.class)
    public static class Song {
        @Field
        private String artist;
        @Field
        private String title;
        @Field("Length of Song")
        private String length;
        
        Accessor methods below...
    }
```

Now in order for the parser to know what domain models that are annotated you need to define a `AnnotatedObjectMappingStore`.  This class you need to set a list of packages that contain your classes that are annotated.
```
        AnnotatedObjectMappingStore objectMappingStore = new AnnotatedObjectMappingStore();
        objectMappingStore.setPackages(Arrays.asList("flapjack.example"));
```

All we should have left now is configuring our `RecordParser`...
```
        RecordParserImpl recordParser = new RecordParserImpl();
        recordParser.setRecordLayoutResolver(new SameRecordLayoutResolver(SongRecordLayout.class));
        recordParser.setRecordFactoryResolver(new SameRecordFactoryResolver(SongFactory.class));
        recordParser.setObjectMappingStore(objectMappingStore);
```

now just parse the data:
```
        String records = "Coldplay  Clocks    03:45";

        LineRecordReader recordReader = new LineRecordReader(new ByteArrayInputStream(records.getBytes()));
        ParseResult result = recordParser.parse(recordReader);
```