# {{ site.Params.brand }} — {{ site.Params.artisan }}

{{ site.Params.tagline }}

Affûtage artisanal (rémouleur) en {{ site.Params.zone }} ({{ site.Params.zoneDetail }}).

## Contact

- Téléphone / SMS : {{ site.Params.phone }}
- E-mail : {{ site.Params.email }}
- Carte : {{ site.Params.mapsUrl }}
- Facebook : {{ site.Params.facebook }}
- Instagram : {{ site.Params.instagram }}

## Ce que j'affûte

{{- range hugo.Data.services.items }}
- **{{ .title }}** — {{ .description }}
{{- end }}

## Comment ça marche

{{- range hugo.Data.process.steps }}
{{ .number }}. **{{ .title }}** — {{ .description }}
{{- end }}

## Pour qui

{{- range hugo.Data.audiences.items }}
### {{ .title }}
{{- range .points }}
- {{ . }}
{{- end }}
{{- end }}

## Où me trouver

{{- range hugo.Data.location.modes }}
### {{ .title }}
{{ .description }}
{{- end }}

{{- with hugo.Data.location.depots }}
### {{ .title }}
{{ .intro }}
{{- range .items }}
- [{{ .name }}]({{ .maps_url }}) — {{ .place }}
{{- end }}
{{- end }}

## Planning

Consulter le calendrier des tournées et marchés sur {{ site.BaseURL }}#planning et prendre rendez-vous au {{ site.Params.phone }}.
