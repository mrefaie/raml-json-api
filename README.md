# raml-json-api
RAML-JSON-API PHP-code generator for different FrameWorks aka Laravel/Yii/Symfony etc

## Yii2 Configuration

Use sample RAML file from the root (the same file is in the tests codeception directory)

The ```version``` root property !required
```RAML
version: v1
```
converts to /modules/v1/ directory.

The ```uses``` root property - !required
```RAML
uses:
  FrameWork: yii
```
creates dir/file structure for Yii2 FrameWork

Types ``` ID, Type, Data``` are special helper types
```RAML
  ID:
    type: integer
    required: true
  Type:
    type: string
    required: true
    minLength: 1
    maxLength: 255
  Data:
    type: object
    required: true
```

Special data type ``` RelationshipsDataItem ```  
```RAML
  RelationshipsDataItem:
    type: object
    properties:
      id: ID
      type: Type
```
defined in every relationship custom type

Attributes ```*Attributes``` are defined for every Object ex.:
```RAML
  RubricAttributes:
    description: Rubric attributes description
    type: object
    properties:
      name_rubric:
        type: string
        required: true
        maxLength: 500
      url:
        type: string
        required: true
        maxLength: 255
      meta_title:
        type: string
        required: false
        maxLength: 255
      meta_description:
        type: string
        required: false
        maxLength: 255
      show_menu:
        type: boolean
        required: true
      publish_rss:
        type: boolean
        required: true
      post_aggregator:
        type: boolean
        required: true
      display_tape:
        type: boolean
        required: true
```

Relationships type definition semantics ```*Relationships```
```RAML
  TagsRelationships:
    description: Tag relationship description
    type: object
    properties:
      data:
        type: DataArray
        items:
          type: RelationshipsDataItem
```

The complete composite Object looks like this: 
```RAML
  Rubric:
    type: object
    properties:
      type: Type
      id: ID
      attributes: RubricAttributes
      relationships: TagsRelationships
```