{{ range .  }}

# {{.Name}}

{{-  if .Folders}}
{{- range .Folders}}

---

## Folder: {{.Name}}
{{-  range .Requests }}

---

### {{.Name}}

**Method**: {{.Method}}  

**RequestURL**: `{{ .URL }}{{ .Path}}`

{{if .Headers}}
**Headers**: 
    <table>
    <tr>
    <th>Key</th>
    <th>Value</th>
    </tr>
    {{- range .Headers}}
    <tr>
    <td>{{- .Key}}</td>
    <td>`{{- .Value}}`</td>
    </tr>
    {{- end -}}
    </table>
{{- end}}
{{- if .Params}}
**Params**: 
    <table>
    <tr>
    <th>type</th>
    <th>Key</th>
    <th>Value</th>
    </tr>
    {{- range .Params}}
    <tr>
    <td>{{- .type}}</td>
    <td>`{{- .key}}`</td>
    <td>`{{- .value}}`</td>
    </tr>
    {{-  end}}
    </table>
{{- end -}}

{{- if ne .Auth "None" }}

**Authentication Type**:  {{ .Auth}}

{{- if .Token}}

**BearerToken**:  `{{  .Token -}}`

{{ end}}

{{- if and .User .Pass}}

**Username**: `{{  .User}}`
**Password**: `{{  .Pass}}`

{{ end -}}

{{ end}}

{{- if and .RawParams (ne .RawParams "{}")}}
**RawParams:**

```json
{{ .RawParams | html}}
```

{{ if .Ctype}}**ContentType**:  `{{ .Ctype}}` {{ end -}}

{{ end -}}

**Pre Request Script**:

```js
{{ .PreRequestScript | html}}
```

**Test Script**:

```js
{{ .TestScript | html}}
```

{{ end -}}{{ end -}}{{ else}}
{{- range .Requests}}

---

### {{ .Name}}

**Method**: {{ .Method}}  

**RequestURL**:  `{{ .URL}}{{ .Path}}`

{{ if .Headers}}
**Headers**: 
    <table>
    <tr>
    <th>Key</th>
    <th>Value</th>
    </tr>
    {{- range .Headers}}
    <tr>
    <td>{{- .Key}}</td>
    <td>`{{- .Value}}`</td>
    </tr>
    {{- end -}}
    </table>
{{- end}}
{{- if .Params}}
**Params**: 
    <table>
    <tr>
    <th>type</th>
    <th>Key</th>
    <th>Value</th>
    </tr>
    {{- range .Params}}
    <tr>
    <td>{{- .type}}</td>
    <td>`{{- .key}}`</td>
    <td>`{{- .value}}`</td>
    </tr>
    {{-  end}}
    </table>
{{- end -}}
{{ if ne .Auth "None"}}
**Authentication Type**: {{.Auth}}  

{{ if .Token}}**BearerToken**: `{{ .Token}}`{{ end}}

{{ if and .User .Pass}}
Username: `{{ .User}}`  
Password: `{{ .Pass}}`
{{ end}}
{{ end}}
{{ if and .RawParams (ne .RawParams "{}")}}
**RawParams**:

```json
{{ .RawParams | html}}
```

{{ end}}
{{ if .Ctype}}**ContentType**: `{{ .Ctype}}` {{ end}}

**Pre Request Script**: 

```js
{{ .PreRequestScript | html}}
```

**Test Script**: 

```js
{{ .TestScript | html}}
```

{{ end }}{{ end}}{{ end}}

---

Generated by [HoppScotch CLI](https://github.com/hoppscotch/hopp-cli) ❤️