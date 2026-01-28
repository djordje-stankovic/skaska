# Email Setup Instructions - Contact Form

## Opcija 1: EmailJS (Preporučeno - Besplatno)

EmailJS je besplatan servis koji omogućava slanje email-a direktno iz frontend-a bez potrebe za backend serverom.

### Koraci za podešavanje:

1. **Registracija na EmailJS:**
   - Idite na https://www.emailjs.com/
   - Kreirajte besplatan nalog
   - Besplatan plan omogućava 200 email-a mesečno

2. **Podešavanje Email Service:**
   - U EmailJS dashboard-u, idite na "Email Services"
   - Kliknite "Add New Service"
   - **VAŽNO:** Ako koristite Gmail i dobijate grešku "insufficient authentication scopes":
     - **Opcija A (Preporučeno):** Koristite **Gmail SMTP** umesto Gmail API
       - Izaberite "Gmail" ali onda izaberite "SMTP" opciju
       - Unesite vašu Gmail adresu
       - Trebaće vam Gmail App Password (ne obična lozinka)
       - Kako dobiti App Password:
         1. Idite na Google Account → Security
         2. Uključite 2-Step Verification ako nije uključena
         3. Idite na "App passwords" (možda treba da pretražite)
         4. Generišite novi App Password za "Mail"
         5. Koristite taj password u EmailJS
     - **Opcija B:** Koristite drugi email provider (Outlook, Yahoo, Custom SMTP)
       - Outlook obično radi bez problema
       - Ili koristite Custom SMTP sa bilo kojim email providerom
   - Nakon uspešnog povezivanja, zapišite **Service ID** (npr. `service_abc123`)

3. **Kreiranje ili korišćenje Email Template:**
   - Idite na "Email Templates" u levom meniju
   - **Opcija A:** Ako već imate template (npr. "Contact Us"), kliknite na njega da ga otvorite
   - **Opcija B:** Ako želite novi, kliknite "Create New Template"
   - Vaš template treba da koristi placeholders:
     - `{{name}}` - za ime korisnika
     - `{{email}}` - za email korisnika
     - `{{title}}` ili `{{subject}}` - za naslov poruke
     - `{{message}}` - za sadržaj poruke
     - `{{time}}` - za vreme (opciono)
   - **VAŽNO:** Zapišite **Template ID** - možete ga naći:
     - Na vrhu stranice kada otvorite template (npr. `template_xyz789`)
     - Ili u URL-u kada ste na stranici template-a
     - Ili u Settings tab-u template-a

4. **Kako da prilagodite Template:**
   - Kliknite na "Content" tab u template-u
   - Kliknite "Edit Content" dugme (ikonica olovke)
   - Možete koristiti HTML za formatiranje
   - **Preporučeni template za kontakt formu:**
   ```
   <div style="font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto;">
     <h2 style="color: #d4af37;">Nova poruka sa kontakt forme</h2>
     
     <div style="background: #f5f5f5; padding: 20px; border-radius: 5px; margin: 20px 0;">
       <p><strong>Ime:</strong> {{name}}</p>
       <p><strong>Email:</strong> {{email}}</p>
       <p><strong>Naslov:</strong> {{title}}</p>
     </div>
     
     <div style="background: #fff; padding: 20px; border-left: 4px solid #d4af37; margin: 20px 0;">
       <h3 style="color: #333; margin-top: 0;">Poruka:</h3>
       <p style="color: #666; line-height: 1.6; white-space: pre-wrap;">{{message}}</p>
     </div>
     
     <p style="color: #999; font-size: 12px; margin-top: 30px;">
       Poruka poslata: {{time}}
     </p>
   </div>
   ```
   - **Subject linija** (u Settings tab-u):
     ```
     Kontakt forma: {{title}}
     ```
   - **Reply To** (u Settings tab-u):
     ```
     {{email}}
     ```
   - Sačuvajte promene klikom na "Save" dugme

4. **Dobijanje Public Key:**
   - Idite na "Account" → "General"
   - Kopirajte **Public Key** (npr. `abcdefghijklmnop`)

5. **Ažuriranje koda:**
   - Otvorite `skaska/contact.html`
   - Pronađite liniju: `emailjs.init("YOUR_PUBLIC_KEY");`
   - Zamenite `YOUR_PUBLIC_KEY` sa vašim Public Key
   - Pronađite liniju: `emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', ...)`
   - Zamenite `YOUR_SERVICE_ID` sa vašim Service ID
   - Zamenite `YOUR_TEMPLATE_ID` sa vašim Template ID

### Primer ažuriranog koda:
```javascript
emailjs.init("abcdefghijklmnop"); // Vaš Public Key

emailjs.send('service_abc123', 'template_xyz789', {
  from_name: formData.name,
  from_email: formData.email,
  subject: formData.subject,
  message: formData.message
})
```

---

## Rešavanje problema sa Gmail API

Ako dobijate grešku **"Request had insufficient authentication scopes"**:

### Rešenje 1: Koristite Gmail SMTP (Najlakše)
1. U EmailJS, kada dodajete novi service, izaberite **"Gmail"**
2. Umesto Gmail API, izaberite **"SMTP"** opciju
3. Unesite vašu Gmail adresu
4. Za lozinku, koristite **Gmail App Password** (ne običnu lozinku):
   - Idite na: https://myaccount.google.com/security
   - Uključite "2-Step Verification" ako nije uključena
   - Idite na "App passwords" (ili pretražite "app passwords")
   - Generišite novi App Password za "Mail"
   - Koristite taj 16-cifreni password u EmailJS

### Rešenje 2: Koristite Outlook ili drugi provider
- Outlook obično radi bez problema
- Yahoo takođe podržava SMTP
- Bilo koji email provider sa SMTP podrškom

### Rešenje 3: Custom SMTP
Ako imate bilo koji email sa SMTP pristupom:
- SMTP Host: (npr. `smtp.gmail.com` za Gmail, `smtp-mail.outlook.com` za Outlook)
- SMTP Port: 587 (TLS) ili 465 (SSL)
- SMTP Username: vaša email adresa
- SMTP Password: App Password ili SMTP lozinka

---

## Opcija 2: PHP Backend (Ako imate server sa PHP podrškom)

Ako imate pristup PHP serveru, možete koristiti PHP skriptu za slanje email-a.

### Koraci:

1. **Kreiranje PHP fajla:**
   - Kreirajte fajl `skaska/send-email.php` sa sledećim kodom:

```php
<?php
header('Content-Type: application/json');
header('Access-Control-Allow-Origin: *');
header('Access-Control-Allow-Methods: POST');
header('Access-Control-Allow-Headers: Content-Type');

if ($_SERVER['REQUEST_METHOD'] !== 'POST') {
    http_response_code(405);
    echo json_encode(['error' => 'Method not allowed']);
    exit;
}

$name = isset($_POST['name']) ? htmlspecialchars($_POST['name']) : '';
$email = isset($_POST['email']) ? htmlspecialchars($_POST['email']) : '';
$subject = isset($_POST['subject']) ? htmlspecialchars($_POST['subject']) : '';
$message = isset($_POST['message']) ? htmlspecialchars($_POST['message']) : '';

if (empty($name) || empty($email) || empty($subject) || empty($message)) {
    http_response_code(400);
    echo json_encode(['error' => 'All fields are required']);
    exit;
}

// Email settings
$to = 'marko@skaskabrandy.com'; // Vaš email
$email_subject = "Contact Form: " . $subject;
$email_body = "Name: $name\n";
$email_body .= "Email: $email\n\n";
$email_body .= "Message:\n$message";
$headers = "From: $email\r\n";
$headers .= "Reply-To: $email\r\n";

if (mail($to, $email_subject, $email_body, $headers)) {
    echo json_encode(['success' => true, 'message' => 'Email sent successfully']);
} else {
    http_response_code(500);
    echo json_encode(['error' => 'Failed to send email']);
}
?>
```

2. **Ažuriranje HTML forme:**
   - U `contact.html`, promenite JavaScript kod da koristi fetch API:

```javascript
document.getElementById('contactForm').addEventListener('submit', function(event) {
  event.preventDefault();
  
  const formData = new FormData(this);
  
  fetch('send-email.php', {
    method: 'POST',
    body: formData
  })
  .then(response => response.json())
  .then(data => {
    if (data.success) {
      // Success message
      alert('Message sent successfully!');
      this.reset();
    } else {
      // Error message
      alert('Error: ' + data.error);
    }
  })
  .catch(error => {
    console.error('Error:', error);
    alert('Error sending message. Please try again.');
  });
});
```

---

## Opcija 3: Formspree (Alternativa)

Formspree je još jedan besplatan servis sličan EmailJS.

1. Idite na https://formspree.io/
2. Registrujte se i kreirajte novi form
3. Dobijete endpoint URL (npr. `https://formspree.io/f/your-form-id`)
4. U `contact.html`, promenite form action:
   ```html
   <form action="https://formspree.io/f/your-form-id" method="POST">
   ```

---

## Preporuka

**EmailJS** je najlakše rešenje jer:
- Ne zahteva backend server
- Besplatno je (200 email-a/mesec)
- Lako se integriše
- Radi direktno iz frontend-a

Samo zamenite tri vrednosti u `contact.html`:
1. `YOUR_PUBLIC_KEY` → Vaš EmailJS Public Key
2. `YOUR_SERVICE_ID` → Vaš EmailJS Service ID  
3. `YOUR_TEMPLATE_ID` → Vaš EmailJS Template ID
