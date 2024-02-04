---
source-git-commit: 0332be5688f9d0375d1dba97c39a87d0e8d28c52
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 4%

---
# Creërend Typologieregel om lijst-Unsubscribe met één klik te steunen:

**1. Maak de nieuwe typologieregel:**
* Klik in de navigatiestructuur op &quot;nieuw&quot; om een nieuwe typologie te maken

![afbeelding](/help/assets/CreatingTypologyRules1.png)

**2. Ga om de typologieregel te vormen te werk:**
* Type regel: Besturing
* Fase: Bij het begin van de doelwitten
* Kanaal: E-mail
* Niveau: uw keuze
* Actief


![afbeelding](/help/assets/CreatingTypologyRules2.png)


**Code javascript of the Typology rule:**


>[!NOTE]
>
>De hieronder beschreven code moet alleen als voorbeeld worden gebruikt.
>In dit voorbeeld wordt beschreven hoe u:
>* Configureer een URL List-Unsubscribe en voeg de kopteksten toe of voeg de bestaande mailto toe: parameters en vervang deze door: &lt;mailto..>>, https://...
>* Toevoegen in de header List-Unsubscribe-Post
>In het voorbeeld van de post-URL wordt var headerUnsubUrl = &quot;https://campmomentumv7-mkt-prod3.campaign.adobe.com/webApp/unsubNoClick?id=&lt;%= receited.cryptedId %>&quot; geselecteerd
>* U kunt andere parameters toevoegen (zoals &amp;service = ...)
>


```
// Function to add or replace a header in the provided headers 
function addHeader(headers, header, value)  { 
    
  // Create the new header line 
  var headerLine = header + ": " + value; 
    
  // Create a regular expression to find the specified header 
  var regExp = new RegExp(header + ":(.*)$", "i") 
    
  // Split the headers into individual lines 
  var headerLines = headers.split("\n"); 
    
  // Loop through each line 
  for (var i=0; i < headerLines.length; i++) { 
      
    // Check if the specified header exists 
    var match = headerLines[i].match(regExp) 
      
    // If it exists 
    if ( match != null ) { 
        
      // Replace the existing header line 
      headerLines[i] = headerLine; 
        
      // Return the modified headers 
      return headerLines.join("\n"); 
    } 
  } 
    
  // If the header does not exist, add the new header line 
  headerLines.push(headerLine); 
    
  // Return the modified headers 
  return headerLines.join("\n"); 
} 
  
// Function to get the value of a specified header from the provided headers 
function getHeader(headers, header) { 
    
  // Create a regular expression to find the specified header 
  var regExp = new RegExp(header + ":(.*)$", "i") 
    
  // Split the headers into individual lines 
  var headerLines = headers.split("\n"); 
    
  // Loop each line 
  for each (line in headerLines) { 
      
    // Check if the specified header exists 
    var match = line.match(regExp); 
      
    // If it exists 
    if ( match != null ) { 
        
      // Return the header value, removing leading whitespace 
      return match[1].replace(/^\s*/, ""); 
    } 
  } 
    
  // If the header does not exist, return an empty string 
  return ""; 
} 
  
  
// Define the unsubscribe URL 
var headerUnsubUrl = "https://campmomentumv7-mkt-prod3.campaign.adobe.com/webApp/unsubNoClick?id=<%= recipient.cryptedId %>"; 
  
// Get the value of the List-Unsubscribe header 
var headerUnsub = getHeader(delivery.mailParameters.headers, "List-Unsubscribe"); 
  
// If the List-Unsubscribe header does not exist 
if ( headerUnsub === "" ) { 
  // Add the List-Unsubscribe header 
  delivery.mailParameters.headers = addHeader(delivery.mailParameters.headers, "List-Unsubscribe", "<"+headerUnsubUrl+">"); 
} 
// If the List-Unsubscribe header exists and contains 'mailto' 
else if(headerUnsub.search('mailto')){ 
  // Replace the existing List-Unsubscribe header 
  delivery.mailParameters.headers = addHeader(delivery.mailParameters.headers, "List-Unsubscribe", "<"+headerUnsubUrl+">"); 
} 
  
// Get the value of the List-Unsubscribe-Post header 
var headerUnsubPost = getHeader(delivery.mailParameters.headers, "List-Unsubscribe-Post"); 
  
// If the List-Unsubscribe-Post header does not exist 
if ( headerUnsubPost === "" ) { 
  // Add the List-Unsubscribe-Post header 
  delivery.mailParameters.headers = addHeader(delivery.mailParameters.headers, "List-Unsubscribe-Post", "List-Unsubscribe=One-Click"); 
} 
  
// Return true to indicate success 
return true; 
```


![afbeelding](/help/assets/CreatingTypologyRules3.png)

**3. Voeg uw nieuwe regel aan een Typologie aan een e-mail (Standaard typologie is ok) toe:**

![afbeelding](/help/assets/CreatingTypologyRules4.png)

**4. Bereid een nieuwe levering voor (verifieer dat de Extra kopballen SMTP in leveringsbezit leeg is)**

![afbeelding](/help/assets/CreatingTypologyRules5.png)

**5. Controleer tijdens de voorbereiding van de levering of de nieuwe typologieregel is toegepast.**

![afbeelding](/help/assets/CreatingTypologyRules6.png)



**6. Bevestig dat lijst-unsubscribe aanwezig is.**

![afbeelding](/help/assets/CreatingTypologyRules7.png)
