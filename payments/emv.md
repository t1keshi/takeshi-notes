Previous: [Payment Technology](payments.md)  

# EMV

Three certification levels defined by EMVco:

### Level 1 (L1) - Hardware & Physical Layer

Electrical interfaces, RF/contact antennas, signal timing, and APDU transport protocols (ISO 7816 for contact chip, ISO 14443 for contactless). Certified by EMVCo every 4 years.

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


### Level 3 (L3) - End-to-End Payment Application

Full solution integration: POS application, PIN entry, ISO 8583 host messaging, and acquirer/processor approval.
