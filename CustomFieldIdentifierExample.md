[Source Code](http://github.com/born2snipe/flapjack/tree/master/flapjack-example/src/test/java/flapjack/example/CustomFieldIdentifierTest.java)

```
    /**
     * This class creates the field identifier for a specific FieldDefinition
     */
    private static class ReverseDescriptionIdGenerator implements MappedFieldIdGenerator {
        public String generate(FieldDefinition fieldDef) {
            StringBuilder builder = new StringBuilder();
            char[] chars = fieldDef.getName().toCharArray();
            for (int i = chars.length - 1; i >= 0; i--) {
                builder.append(chars[i]);
            }
            return builder.toString();
        }
    }
```

```
        /**
         *  Configure the RecordFieldParser to use the custom field id generator
         */
        ByteMapRecordFieldParser fieldParser = new ByteMapRecordFieldParser();
        fieldParser.setFieldIdGenerator(new ReverseDescriptionIdGenerator());
```