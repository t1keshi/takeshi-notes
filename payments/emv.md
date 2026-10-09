Previous: [Payment Technology](payments.md)  

# EMV

- the first specifications were published in 1995  
- first EMV cards were rolled out in Europe in 1999 

EMVCo is the global technical body that manages and mantains the specifications and associated processes.  

EMVCo is jointly owned by American Express, Discover, JCB, MasterCard, UnionPay and Visa.  

Develop and maintain the EMV chip specifications and ensure their ongoing interoperability and compatibility with the global payment industry.  

The specifications for EMV transactions are defined based on several different standards.


# ISO 7816

This is a standard that defines how chip cards work at the eletronic level, including their interface with the terminal and the commands that can be sent to the chip to reuqest information or perfom some transactions. It also defines the basic software functions that are common to all chip cards.  


### EMV Level 1 (L1) - Hardware & Physical Layer

Electrical interfaces, RF/contact antennas, signal timing, and APDU transport protocols (ISO 7816 for contact chip, ISO 14443 for contactless). Certified by EMVCo every 4 years.

This specification defines the electrical and physical characteristics of the payment cards, including the design and layout of the cards, chip and contacts. It is also called the packet level because it is responsible for defining the physical and electrical characteristics of the communication interface between the payment card an the payment terminal.

This include things like the voltage levels, timing requirements and signals encoding used to transmit data between the card and the terminal.

The level 1 specifications also defines the mechanical and contact arrangments for the physical interface between the card and the terminal, including the number and location of the contact points on the card and terminal.


### Level 2 (L2) - Application Kernel / Card logic

Software rules governing card-to-terminal dialogue: AID selection, cryptographic authentication (SDA, DDA, CDA), risk management, and cryptogram generation (ARQC/TC). Certified by EMVCo and card brands.

A Level 2 Kernel is a certified, standalone software library that implements the technical rules for coomunicating with a smart card application.

Contact L2 Kernel

- Evaluates contact chip cards inserted into the slot (CAM0) according to EMVCo Books 1-4.
- Common across terminal models (e.g., Ingenico's EMV contact kernel covered by a single Letter of Approval across the device family)

Contactless L2 Kernels

Because each card brand maintains proprietary contactless specifications, terminals use dedicated brand kernels.

- Kernel 2: Mastercard Contactless/PayPass (M/Chip)  
- Kernel 3: Visa payWave/VCPS  
- Kernel 4: American Express ExpressPay
- Kernel 6: Discover DPAS
- Kernel 5/7/White-Label: JCB J/Speedy, UnionPay qUICS, PURE, or CPACE

Every chip card is compatible with this level.

The main purpose of these specifications is to ensure interoperability between various payment networks and make it possible for any payment terminal in the world to process transactions of any chip card, regardless of the payment network.

This specification defines the software requirements for payment applications that run on payment cards. It includes requirements for the cards, user interface, transaction processing and security features. 


### Level 3 (L3) - End-to-End Payment Application

Full solution integration: POS application, PIN entry, ISO 8583 host messaging, and acquirer/processor approval.


### Network

It defines how each payment network can have differentiated applications, allowing them to manage risk in their own way and offer personalised features to their customers. They also defines the protocols for message formatiing, data exchange and authentication.

#

So this is the basic structure of various levels present in EMV chip transactions.  

ISO7816
Here the electronic level. ISO 7816 is managed by ISO

EMV Level 1
EMV Level 2
The packet level EMV Level 1 and application level EMV Level 2 are both managed by EMVCO and are

Network
The payment network specific level is managed by each payment network on its own.

- VISA: Visa Integrated Circuit Card Specification
- MASTERCARD: M/Chip 4 Card Application Specifications

# EMVCo specifications

These specifications will be used when a transaction is made by inserting the card into the terminal. Aside from that, we have EMV chip contactless specifications which will be used when a transaction is made by tapping the card on the terminal or when making near-field communications (NFC). NFC is using a device like your mobile phone.

And EMV chip personalization specifications, which will be used when the card is being manufactured. They provide a set of guidelines and rules that define how an EMV chip cad should be personalized with a cardholder's information, such as the card holder's name, account number, expiration date and other necessary information.

These specifications ensure that the card and terminal communicate with each other in a standard way.

In addition to these, we also have mobile specifications wich define the technical requirements for enabling contactless payments using a mobile device, typically a smartphone or a smartwatch.

Some of the key features of the EMV specifications for a mobile device include the following.

1. tokenization: to enhance security payment credentials are replaced with a token, which is a unique digital identifier that is unique to the mobile device, transaction and payment network.  
- this means that if a token is intercepted or stolen, it cannot be used for any transaction
- When a merchant processes the credit card of a customer, the primary account number is substituted with a token. The merchant can apply the toke ID to retain records fo the customer. For example, the token ID is this which is connected to Will Smith. The token ID is then transferred to the payment processor who detokenize the ID and confirms the payment.

2. 3-D Secure: this requires the user to enter an additional password or some other authentication factor to verify their identity before a payment can be completed. In the context of mobile payments, 3D secure is typically implemented using an app or a browser that is installed on the mobile device. When a customer initiates a payment, they are prompted to enter their 3-D secure password or authenticate using other factors such as fingerprint or facil recognition.

3. Quick Response Code: which is a two dimensional barcode that contains payment related information. It is designed to facilitate mobile payments, allowing consumers to make transactions using their mobile devices. The QR code contains data such as the merchant's identification number, the transaction amount and other relevant details.

4. Secure Element: Contactless payment require a secure element to store and protect the payment credentials. This secure element can be a hardware component within the mobile device or a cloud based solution.

# Segregation of EMV Standards and technologies

Three categories:

1. Face-to-Face Transactions  

- EMV contact specifications
- EMV contactless specifications  
- EMV mobile based specifications  
- EMV QR code specifications  
- Wearable device specifications

2. Remote Transactions  

- e-commerce websites: EMV Secure Remote Commerce specifications
- Authentication of the cardholder: EMV 3-D Secure Specifications.

3. Authentication of the customer

- CDCVM (Consumer Device Cardholder Verification Method) where the fingerprint, pattern or password mechanisms of your mobile device can be used in the card transaction processe and some other options such as security evaluations for software based mobile payments and payment tokenization standards.

# Benefits EMV chip card vs Magnetic Stripes

- magnetic stripe cards have no processing capacity, as all the data on the card is stored on the magnetic stripe, which is a static data storage midium. The magnetic stripe cardscannot generate dynamic codes or perfom any processing tasks on their own
- EMV chip cars have a microprocessor embedded in the card which allows them to perfom processing tasks and generate dynamic codes for every transaction
- Magnetic stripe card have limited data storage capacity, which can limit their functionality as well as usability
- EMV chip cards can store much more data and can be used for a variety of purposes such as loyalty programs or rewards
- Magnetic stripe has lower security - as the data stored on the magnetic can easily copied or skimmed, much like the CV on the back of these cards is a static code that can be used for fraud
- EMV card generates a unique transaction code for every purchase, making it much more difficult to clone or counterfeit
- The magnetic stripe also has a poor signature verification. Magnetic stripe cards rely on a signature as a form of verification, but signature vverification is often unreliable due to several factors, such as the poor quality of the signature and incosistent signature styles. This can make it difficult to compare signatures and authenticate the transactions
- There are also limitations of the issuer approval process in magnetic stripe cards, transactions exceeding the merchant floor limit, which is a predefined amount set on a merchant, can only be authorized by the issuer approval process, meaning every time a high value transaction above the merchant floor limit is made through this card, it will be authorized by the issuer, which includes verifying the identity of the customer, running credit checks and determining the credit limit, all of whoch can take a considerable amount of time.
- EMV chip cards, on the other hand, have a more streamlined and automated approval process, which can significantly reduce the time and resources required to issue a card.


- EMV cards do not require to be in a fixed design like magnetic stripe cards
- It is the chip embedded in the EMV card that is being used to run a payment application and is even capable of doing the authentication
- It can even be taken out and put in the SIM slot of our mobile phones and the phone can be used as a card
- this provides greater flexibility for design and security as it i much more difficult to replicate or counterfeit.  
- EMV chip cards have the ability to process transactions offline which can be useful in areas where there is no reliable network connection
- In offline mode, the card uses data stored on the chip to authenticate the transaction
- EMV chip cards reduce risk of payment transaction by providing the issuer as well as the acquirer with the tools to manage risk in card payment transactions. This is accomplished bt allowing the issuer to embed risk controls in the chip card and the acquirer in the terminal. The risk controls issuer action codes and terminal action codes, assist the chip card and terminal in determing: how to process a card payment transaction transaction that is maybe offline or online or declined on line would refer to the process where transaction is authenticated by the issuer.
- EMV cards have better card authentication: EMV chip cards use a combination of cryptographic techniques and digital signatures to authenticate the card, which can be authenticated by both the issuer and the terminal to ensure that it is not a couterfeit. Hence, they definitely provide a better card authentication mechanism than the magnetic stripe cards.



