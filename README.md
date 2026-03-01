# WhatsApp Baileys

<p align="center">
  <img src="https://raw.githubusercontent.com/than-xs/than-xs/refs/heads/main/image.png" alt="image" />
</p>

**WhatsApp Baileys** is an open-source library built to help developers create automation systems and integrations with WhatsApp efficiently and directly through WebSocket — without requiring a browser instance.

Designed with stability and modularity in mind, this library supports message management, chat handling, group administration, interactive messages, event systems, polls, product catalogs, and more. It is suitable for building bots, business automation, customer service systems, and scalable communication platforms.

Baileys continues to receive improvements focused on authentication stability, pairing reliability, and compatibility with the latest WhatsApp multi-device architecture.

---

## ✨ Main Features & Advantages

- Automatic and custom pairing support
- Improved authentication & reconnection stability
- Interactive messages, native flow, and action buttons
- Album, event, poll, and product message support
- Efficient automatic session management
- Compatible with WhatsApp Multi-Device
- Lightweight, modular, and easy to integrate
- Suitable for bots, automation, and business systems
- Comprehensive examples for easier development

---

## 🚀 Getting Started

Install the library using your preferred package manager, configure your authentication/session storage, and start building automation workflows using the provided examples.

Leverage interactive messaging, newsletter tools, and session handling to build stable, production-ready solutions.

---

# 📦 Additional Functions (Simple Examples)

## Label Group
Tag or label group members.

```javascript
await sock.setLabelGroup(jid, string)
```
---
### Check Channel ID
Get channel ID from URL

```javascript
await sock.newsletterFromUrl(url)
```
Result (JSON)
```json
{
  "name": "Name Channel",
  "id": "Channel ID",
  "state": "Status Channel",
  "subscribers": "Followers",
  "verification": "UNVERIFIED",
  "creation_time": 1728547155,
  "description": "Description Channel"
}
```
---
### Check Banned Number
Check the status of a WhatsApp number

```javascript
sock.checkBan(jid)
```
---

## 📤 SendMessage Documentation

### Status Mention (Group & Private)

```javascript
await sock.sendStatusMention(content, jid);
```

### Group Status Message V2

```javascript
await sock.sendMessage(jid, {
     groupStatusMessage: {
          text: "Hello world"
     }
});
```

### Album Message (Multiple Images)

```javascript
await sock.sendMessage(jid, {
  albumMessage: [
    { image: buffer1, caption: "First image" },
    { image: { url: "https://example.com/img.jpg" }, caption: "Second image" }
  ]
});
```

### Event Message

```javascript
await sock.sendMessage(jid, {
  eventMessage: {
    isCanceled: false,
    name: "Event Title",
    description: "Event description",
    location: {
      degreesLatitude: 0,
      degreesLongitude: 0,
      name: "Location Name"
    },
    joinLink: "https://call.whatsapp.com/video/example",
    startTime: "1763019000",
    endTime: "1763026200",
    extraGuestsAllowed: false
  }
});
```

### Poll Result Message

```javascript
await sock.sendMessage(jid, {
  pollResultMessage: {
    name: "Poll Title",
    pollVotes: [
      { optionName: "Option 1", optionVoteCount: "10" },
      { optionName: "Option 2", optionVoteCount: "5" }
    ]
  }
});
```

### Simple Interactive Message
Send basic interactive messages with copy button functionality :

```javascript
await sock.sendMessage(jid, {
  interactiveMessage: {
    header: "Header",
    title: "Title",
    footer: "Footer",
    buttons: [
      {
        name: "cta_copy",
        buttonParamsJson: JSON.stringify({
          display_text: "Copy Code",
          id: "123",
          copy_code: "ABC123"
        })
      }
    ]
  }
});
```

### Interactive Message with Native Flow
Send interactive messages with buttons, copy actions, and native flow features :

```javascript
await sock.sendMessage(jid, {    
    interactiveMessage: {      
        header: "Hello world",
        title: "Hello world",      
        footer: "telegram : @thanror",      
        image: { url: "https://example.com/image.jpg" },      
        nativeFlowMessage: {        
            messageParamsJson: JSON.stringify({          
                limited_time_offer: {            
                    text: "yeah",            
                    url: "https://t.me/thanror",            
                    copy_code: "xs-meta",            
                    expiration_time: Date.now() * 999          
                },          
                bottom_sheet: {            
                    in_thread_buttons_limit: 2,            
                    divider_indices: [1, 2, 3, 4, 5, 999],            
                    list_title: "than.xs",            
                    button_title: "than.xs"          
                },          
                tap_target_configuration: {            
                    title: " X ",            
                    description: "nande-nande",            
                    canonical_url: "https://t.me/thanror",            
                    domain: "shop.example.com",            
                    button_index: 0          
                }        
            }),        
            buttons: [          
                {            
                    name: "single_select",            
                    buttonParamsJson: JSON.stringify({              
                        has_multiple_buttons: true            
                    })          
                },          
                {            
                    name: "call_permission_request",            
                    buttonParamsJson: JSON.stringify({              
                        has_multiple_buttons: true            
                    })          
                },          
                {            
                    name: "single_select",            
                    buttonParamsJson: JSON.stringify({              
                        title: "Hello world",              
                        sections: [                
                            {                  
                                title: "title",                  
                                highlight_label: "label",                  
                                rows: [                    
                                    {                      
                                        title: "@thanror",                      
                                        description: "love you",                      
                                        id: "row_2"                    
                                    }                  
                                ]                
                            }              
                        ],              
                        has_multiple_buttons: true            
                    })          
                },          
                {            
                    name: "cta_copy",            
                    buttonParamsJson: JSON.stringify({              
                        display_text: "copy code",              
                        id: "123456789",              
                        copy_code: "ABC123XYZ"            
                    })          
                }        
            ]      
        }    
    }  
}, { quoted: m });
```

### Interactive Message with Thumbnail
Send interactive messages with thumbnail image and copy button :

```javascript
await sock.sendMessage(jid, {
    interactiveMessage: {
        header: "Hello world",
        title: "Hello world",
        footer: "telegram : @thanror",
        image: { url: "https://example.com/image.jpg" },
        buttons: [
            {
                name: "cta_copy",
                buttonParamsJson: JSON.stringify({
                    display_text: "copy code",
                    id: "123456789",
                    copy_code: "ABC123XYZ"
                })
            }
        ]
    }
}, { quoted: m });
```

### Product Message
Send product catalog messages with buttons and merchant information:

```javascript
await sock.sendMessage(jid, {
    productMessage: {
        title: "Produk Contoh",
        description: "Ini adalah deskripsi produk",
        thumbnail: { url: "https://example.com/image.jpg" },
        productId: "PROD001",
        retailerId: "RETAIL001",
        url: "https://example.com/product",
        body: "Detail produk",
        footer: "Harga spesial",
        priceAmount1000: 50000,
        currencyCode: "USD",
        buttons: [
            {
                name: "cta_url",
                buttonParamsJson: JSON.stringify({
                    display_text: "Beli Sekarang",
                    url: "https://example.com/buy"
                })
            }
        ]
    }
}, { quoted: m });
```

### Interactive Message with Document Buffer
Send interactive messages with document from buffer (file system) - **Note: Documents only support buffer**:

```javascript
await sock.sendMessage(jid, {
    interactiveMessage: {
        header: "Hello world",
        title: "Hello world",
        footer: "telegram : @thanror",
        document: fs.readFileSync("./package.json"),
        mimetype: "application/pdf",
        fileName: "document.pdf",
        jpegThumbnail: fs.readFileSync("./document.jpeg"),
        contextInfo: {
            mentionedJid: [jid],
            forwardingScore: 777,
            isForwarded: false
        },
        externalAdReply: {
            title: "than.xs",
            body: "xs.company",
            mediaType: 3,
            thumbnailUrl: "https://example.com/image.jpg",
            mediaUrl: " X ",
            sourceUrl: "https://t.me/thanror",
            showAdAttribution: true,
            renderLargerThumbnail: false         
        },
        buttons: [
            {
                name: "cta_url",
                buttonParamsJson: JSON.stringify({
                    display_text: "Telegram",
                    url: "https://t.me/thanror",
                    merchant_url: "https://t.me/thanror"
                })
            }
        ]
    }
}, { quoted: m });
```

### Interactive Message with Document Buffer (Simple)
Send interactive messages with document from buffer (file system) without contextInfo and externalAdReply - **Note: Documents only support buffer**:

```javascript
await sock.sendMessage(jid, {
    interactiveMessage: {
        header: "Hello world",
        title: "Hello world",
        footer: "telegram : @thanror",
        document: fs.readFileSync("./package.json"),
        mimetype: "application/pdf",
        fileName: "document.pdf",
        jpegThumbnail: fs.readFileSync("./document.jpeg"),
        buttons: [
            {
                name: "cta_url",
                buttonParamsJson: JSON.stringify({
                    display_text: "Telegram",
                    url: "https://t.me/thanror",
                    merchant_url: "https://t.me/thanror"
                })
            }
        ]
    }
}, { quoted: m });
```

### Request Payment Message
Send payment request messages with custom background and sticker:

```javascript
let quotedType = m.quoted?.mtype || '';
let quotedContent = JSON.stringify({ [quotedType]: m.quoted }, null, 2);

await sock.sendMessage(jid, {
    requestPaymentMessage: {
        currency: "IDR",
        amount: 10000000,
        from: m.sender,
        sticker: JSON.parse(quotedContent),
        background: {
            id: "100",
            fileLength: "0",
            width: 1000,
            height: 1000,
            mimetype: "image/webp",
            placeholderArgb: 0xFF00FFFF,
            textArgb: 0xFFFFFFFF,     
            subtextArgb: 0xFFAA00FF   
        }
    }
}, { quoted: m });
```

---

## Why Choose WhatsApp Baileys?

Because this library offers high stability, full features, and an actively improved pairing process. It is ideal for developers aiming to create professional and secure WhatsApp automation solutions. Support for the latest WhatsApp features ensures compatibility with platform updates.

---

### Technical Notes

- Supports custom pairing codes that are stable and secure
- Fixes previous issues related to pairing and authentication
- Features interactive messages and action buttons for dynamic menu creation
- Automatic and efficient session management for long-term stability
- Compatible with the latest multi-device features from WhatsApp
- Easy to integrate and customize based on your needs
- Perfect for developing bots, customer service automation, and other communication applications
- Has 1 newsletter follow, only the developer's WhatsApp channel : [WhatsApp Channel](https://whatsapp.com/channel/0029VbAjdOlIt5rqKMzZiQ0s)

---

For complete documentation, installation guides, and implementation examples, please visit the official repository and community forums. We continually update and improve this library to meet the needs of developers and users of modern WhatsApp automation solutions.

**Thank you for choosing WhatsApp Baileys as your WhatsApp automation solution!**


---


### Contact Developer

For questions, support, or collaboration, feel free to contact the developer:

- **Telegram** : [Telegram Contact](https://t.me/thanror)
- **Channel WhatsApp** : [Channel WhatsApp](https://whatsapp.com/channel/0029VbAjdOlIt5rqKMzZiQ0s)