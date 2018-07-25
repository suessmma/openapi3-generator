<tr>
  <td>{{tree path}}{{propName}} {{#if required}}<strong>(required)</strong>{{/if}}</td>
  <td>
    {{prop.type}}
    {{~#if prop.anyOf}}anyOf{{~/if}}
    {{~#if prop.oneOf}}oneOf{{~/if}}
    {{~#if prop.items.type}}({{prop.items.type}}){{~/if}}
  </td>
  <td>{{prop.in}}</td>
  <td>{{{prop.schema.description}}}</td>
  <td>{{{acceptedValues prop.enum}}}</td>
</tr>
{{#each prop.anyOf}}
{{> paramProp prop=. propName=@key path=(buildPath ../propName ../path @key)}}
{{/each}}
{{#each prop.oneOf}}
  {{> paramProp prop=. propName=@key path=(buildPath ../propName ../path @key)}}
{{/each}}
{{#each prop.properties}}
{{> paramProp prop=. propName=@key required=(isRequired ../prop @key) path=(buildPath ../propName ../path @key)}}
{{/each}}
{{#each prop.additionalProperties.properties}}
{{> paramProp prop=. propName=@key required=(isRequired ../prop.additionalProperties @key) path=(buildPath ../propName ../path @key)}}
{{/each}}
{{#each prop.items.properties}}
{{> paramProp prop=. propName=@key required=(isRequired ../prop.items @key) path=(buildPath ../propName ../path @key)}}
{{/each}}