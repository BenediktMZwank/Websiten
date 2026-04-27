# EmailJS Shop Template

Dieses Template passt zum Bestellformular im Shop und nutzt genau die Felder, die aus der Website gesendet werden.

## Empfohlener Betreff

```text
Neue Schlaegerbestellung: {{product}} x{{quantity}} - {{name}}
```

## Empfohlener HTML-Inhalt

```html
<div style="margin:0;padding:24px;background:#f4f7f2;font-family:Arial,Helvetica,sans-serif;color:#153824;">
  <div style="max-width:680px;margin:0 auto;background:#ffffff;border:1px solid #d7e6da;border-radius:20px;overflow:hidden;">
    <div style="padding:28px 32px;background:linear-gradient(135deg,#153824,#2b9d5e);color:#f8fff9;">
      <p style="margin:0 0 8px;font-size:12px;letter-spacing:0.14em;text-transform:uppercase;opacity:0.8;">{{site_name}}</p>
      <h1 style="margin:0;font-size:28px;line-height:1.2;">Neue Schlaegerbestellung</h1>
      <p style="margin:12px 0 0;font-size:15px;line-height:1.6;opacity:0.92;">
        Bestellung auf Rechnung angefragt ueber das Shop-Formular.
      </p>
    </div>

    <div style="padding:28px 32px;">
      <div style="margin-bottom:24px;padding:20px;border-radius:16px;background:#f7fbf8;border:1px solid #e0ece3;">
        <p style="margin:0 0 6px;font-size:12px;letter-spacing:0.12em;text-transform:uppercase;color:#2b9d5e;">Bestellung</p>
        <p style="margin:0;font-size:24px;font-weight:700;color:#153824;">{{product}}</p>
        <p style="margin:10px 0 0;font-size:16px;color:#31543f;">Anzahl: <strong>{{quantity}}</strong></p>
      </div>

      <table role="presentation" style="width:100%;border-collapse:collapse;margin-bottom:24px;">
        <tr>
          <td colspan="2" style="padding:0 0 12px;font-size:12px;letter-spacing:0.12em;text-transform:uppercase;color:#2b9d5e;">Kundendaten</td>
        </tr>
        <tr>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#5a7464;width:180px;">Name</td>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#153824;"><strong>{{name}}</strong></td>
        </tr>
        <tr>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#5a7464;">E-Mail</td>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#153824;">{{email}}</td>
        </tr>
        <tr>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#5a7464;">Telefon</td>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#153824;">{{phone}}</td>
        </tr>
      </table>

      <table role="presentation" style="width:100%;border-collapse:collapse;margin-bottom:24px;">
        <tr>
          <td colspan="2" style="padding:0 0 12px;font-size:12px;letter-spacing:0.12em;text-transform:uppercase;color:#2b9d5e;">Lieferadresse</td>
        </tr>
        <tr>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#5a7464;width:180px;">Strasse</td>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#153824;">{{street}}</td>
        </tr>
        <tr>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#5a7464;">PLZ</td>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#153824;">{{postal_code}}</td>
        </tr>
        <tr>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#5a7464;">Ort</td>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#153824;">{{city}}</td>
        </tr>
        <tr>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#5a7464;">Land</td>
          <td style="padding:10px 0;border-top:1px solid #e7efe9;color:#153824;">{{country}}</td>
        </tr>
      </table>

      <div style="margin-bottom:24px;">
        <p style="margin:0 0 12px;font-size:12px;letter-spacing:0.12em;text-transform:uppercase;color:#2b9d5e;">Nachricht</p>
        <div style="padding:18px;border-radius:16px;background:#f7fbf8;border:1px solid #e0ece3;color:#153824;line-height:1.7;">
          {{message}}
        </div>
      </div>

      <div style="padding:18px;border-radius:16px;background:#fff8e8;border:1px solid #f1deb0;color:#6b5320;">
        <strong>Zahlungsart:</strong> Bestellung auf Rechnung
      </div>
    </div>
  </div>
</div>
```

## Einfache Text-Version

```text
Neue Schlaegerbestellung

Shop: {{site_name}}
Typ: {{request_type}}

Produkt: {{product}}
Anzahl: {{quantity}}

Name: {{name}}
E-Mail: {{email}}
Telefon: {{phone}}

Lieferadresse:
{{street}}
{{postal_code}} {{city}}
{{country}}

Nachricht:
{{message}}

Zahlungsart: Bestellung auf Rechnung
```

## Verwendete Platzhalter

```text
{{site_name}}
{{request_type}}
{{product}}
{{quantity}}
{{name}}
{{email}}
{{phone}}
{{street}}
{{postal_code}}
{{city}}
{{country}}
{{message}}
```

## Empfehlung fuer EmailJS

```text
Template Name: shop-order
From Name: {{name}}
Reply To: {{email}}
```
