# Multiple record types encounted in the same file/stream [SourceCode](http://github.com/born2snipe/flapjack/tree/master/flapjack-example/src/test/java/flapjack/example/DifferentRecordTypeTest.java)

# Record Specification #

### User Record ###
| Name | Position | Length |
|:-----|:---------|:-------|
| Type | 0 | 2 |
| First Name | 2 | 10 |
| Last Name | 12 | 10 |
| Username | 22 | 10 |


### Address Record ###
| Name | Position | Length |
|:-----|:---------|:-------|
| Type | 0 | 2 |
| Address Line | 2 | 20 |
| City | 22 | 15 |
| State | 27 | 2 |


So first we will have to define our record layouts for the two different type of records.
```
    private static class UserRecordLayout extends SimpleRecordLayout {
        private UserRecordLayout() {
            field("Record Type", 2);
            field("First Name", 10);
            field("Last Name", 10);
            field("Username", 10);
        }
    }

    private static class AddressRecordLayout extends SimpleRecordLayout {
        private AddressRecordLayout() {
            field("Record Type", 2);
            field("Address Line", 20);
            field("City", 15);
            field("State", 2);
        }
    }
```

Now since we expecting to encounter 2 different types of record layouts we will need to define a `RecordLayoutResolver`, this will determine what `RecordLayout` should be used for parsing the current record.
```
    private static class BasicRecordLayoutResolver implements RecordLayoutResolver {
        public RecordLayout resolve(byte[] bytes) {
            String code = new String(new byte[]{bytes[0], bytes[1]});
            if ("#1".equals(code)) {
                return new UserRecordLayout();
            } else if ("#2".equals(code)) {
                return new AddressRecordLayout();
            }
            return null;
        }
    }
```

We now need to define our record factories to be used:
```
    private static class UserRecordFactory implements RecordFactory {
        public Object build() {
            return new User();
        }
    }

    private static class AddressRecordFactory implements RecordFactory {
        public Object build() {
            return  new Address();
        }
    }
```

Since we are expecting 2 different types of records we need to define a `RecordFactoryResolver`.
```
    private static class BasicRecordFactoryResolver implements RecordFactoryResolver {
        public RecordFactory resolve(RecordLayout layout) {
            if (layout instanceof UserRecordLayout)
                return new UserRecordFactory();
            else if (layout instanceof AddressRecordLayout)
                return new AddressRecordFactory();
            else
                return null;
        }
    }
```

Next what we need to do is configure our mappings from our fields to our domain model
```
        ObjectMapping userMapping = new ObjectMapping(User.class);
        userMapping.add("First Name", "firstName");
        userMapping.add("Last Name", "lastName");
        userMapping.add("Username", "userName");

        ObjectMapping addressMapping = new ObjectMapping(Address.class);
        addressMapping.add("Address Line", "line");
        addressMapping.add("City", "city");
        addressMapping.add("State", "state");

        ObjectMappingStore objectMappingStore = new ObjectMappingStore();
        objectMappingStore.add(userMapping);
        objectMappingStore.add(addressMapping);
```

All we should have left now is configuring our `RecordParser`...
```
        RecordParserImpl recordParser = new RecordParserImpl();
        recordParser.setRecordLayoutResolver(new BasicRecordLayoutResolver());
        recordParser.setRecordFactoryResolver(new BasicRecordFactoryResolver());
        recordParser.setObjectMappingStore(objectMappingStore);
        recordParser.setIgnoreUnmappedFields(true);
```

now just parse the data:
```
        String records = "#1Joe       Smith     jsmith    \n#21234 Easy St        Chicago        IL";

        LineRecordReader recordReader = new LineRecordReader(new ByteArrayInputStream(records.getBytes()));
        ParseResult result = recordParser.parse(recordReader);
```