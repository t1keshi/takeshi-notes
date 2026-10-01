Previous: [Payments Technology](payments.md)  


# Smart Cards  

- Modern smart card operating systems currently comprise 120000 lines of source code.   
- An important feature of smart cards is that their properties are strongly based on international standards. This is fundamentally important with regard to the usually compulsory need for interoperability.  


# History

The proliferation of plastic cards started in the USA in the early 1950s. The low price of the synthetic material PVC made it possible to produce robust, durable plastic cards that were much more suitable for everyday use than the paper and cardboard cards previously used, which could not adequately withstand mechanical stresses and climatic effects.

The first all-plastic payment card for general use was issued by the **Diners Club** in 1950. It was intended for an exclusive class of individual, and thus also served as a status symbol, allowing the holder to pay with his or her "good name" instead of cash. Initially, only the more select restaurants and hotels accepted these cards, so this type of card came to be known as a **travel and entertainment card**.

The entry of **Visa** and **MasterCard** into the field led to a very rapid proliferation of "plastic money" in the form of credit cards. This occurred first in the USA, with Europe and the rest of the world following a few years later.

Today, credit cards allow travelers to shop without cash everywhere in the world. A **cardholder** is never at a loss for means of payment, yet he or she
avoids exposure to the risk of loss due to theft or other unpredictable hazards, particularly while traveling. Using a credit card also eliminates the tedious task of exchanging currency when traveling abroad. These unique advantages helped credit cards become rapidly established throughout the world.

At first, the functions of these cards were quite simple. They served as data storage media that were secure against forgery and tampering. General information, such as the **card issuer's name**, was printed on the surface, while personal data elements, such as the **cardholder's name** and the **card number**, were embossed. Many cards also had a **signature panel** where the cardholder could sign his or her name for reference.

In these first-generation cards, protection against forgery was provided by visual features, such as security printing and the signature panel. Consequently, the system's security depended quite fundamentally on the quality and conscientiousness of the persons responsible for accepting the cards. However, this did not represent an overwhelming problem, due to the card's initial exclusivity. With the increasing proliferation of card use, these rather rudimentary features no longer proved sufficient, particularly since threats from organized criminals were growing apace.

Increasing handling costs for merchants and banks made a **machine-readable card** necessary, while at the same time, losses suffered by card issuers as the result of customer insolvency and fraud grew from year to year. It became apparent that the security features for protection against fraud and manipulation, as well as the basic functions of the card, had to be expanded and improved.

The first improvement consisted of a **magnetic stripe** on the back of the card, which allowed digital data to be stored on the card in machine-readable form as a supplement to the visual information. This made it possible to minimize the use of **paper receipts**, which were previously essential, although the customer's signature on a paper receipt was still required in traditional credit card applications as a form of personal identification.

However, new approaches that did not require paper receipts could also be devised. **This made it possible to finally achieve the long-standing objective of replacing paper-based transactions by electronic data processing.** This required a different method to be used for user identification, which previously employed the user's signature. The method that has come into widespread general use involves a **secret personal identification number (PIN)** that is compared with a reference number.

However, magnetic-stripe technology has a crucial weakness, which is that the data stored on the stripe can be read, deleted and rewritten at will by anyone with access to the necessary equipment. It is thus unsuitable for storing confidential data. Additional techniques must be used to ensure confidentiality of the data and prevent manipulation of the data. For example, the reference value for the PIN could be stored in the terminal or host system in a secure environment, instead of on the magnetic stripe. **Most systems that employ magnetic-stripe cards thus use online connections to the system's host computer for reasons of security, even though
this generates significant costs for the necessary data transmissions.** In order to reduce costs, it is necessary to find solutions that allow card transactions to be executed **offline** without endangering the security of the system. The development of the **smart card**, combined with the expansion of electronic data-processing systems, has created completely new possibilities for devising such solutions.

Enormous progress in microelectronics in the 1970s made it possible to integrate data storage and processing logic on a single silicon chip measuring a few square millimetres. The idea of incorporating such an integrated circuit into an identification card was contained in a patent application filed by the German inventors **Jurgen Dethloff** and **Helmut Grotrupp** as early as 1968. This was followed in 1970 by a similar patent application by **Kunitaka Arimura** in Japan. However, the first real progress in the development of smart cards came when **Roland Moreno** registered his smart card patents in France in 1974. It was only then that the semiconductor industry was able to supply the necessary integrated circuits at acceptable prices. Nevertheless, many technical problems still had to be solved before the first prototypes, some of which contained several integrated circuit chips, could be transformed into reliable products that could be manufactured in large numbers with adequate quality at a reasonable cost. Since the basic inventions in smart card technology originated in Germany and France, it is not surprising that these countries played the leading roles in the development and marketing of smart cards.

**The great breakthrough was achieved in 1984, when the French PTT (_postal and telecommunications services agency_) successfully carried out a field trial with telephone cards**. In this field trial, smart cards immediately proved to meet all expectations with regard to high reliability and protection against manipulation. Significantly, this breakthrough for smart cards did not come in an area where traditional cards were already used, but in a new application. Introducing a new technology in a new application has the great advantage that compatibility with existing systems does not have to be taken into account, so the capabilities of the new technology can be fully exploited.

A pilot project was conducted in Germany in 1984–85, using telephone cards based on several technologies. Magnetic-stripe cards, optical-storage (holographic) cards and smart cards were used in comparative tests. Smart cards proved to be the winners in this pilot study. In addition to a high degree of reliability and security against manipulation, smart card technology promised the greatest degree of flexibility for future applications. Although the older but less expensive **EPROM** technology was used in the French telephone card chips, more recent **EEPROM** chips were used from the start in the German telephone cards. The latter type of chip does not need an external programming voltage. An unfortunate consequence is that the French and German telephone cards are mutually incompatible. It appears that even after the introduction of the euro, French and German telephone cards will remain unusable in each other's country of origin for at least a while.

Further developments followed the successful trials of telephone cards, first in France and then in Germany, with breathtaking speed. By 1986, several million smart telephone cards were in circulation in France alone. The total rose to nearly 60 million in 1990, and to several hundred million worldwide in 1997. Germany experienced similar progress, with a time lag of about three years. These systems were marketed throughout the world after the successful introduction of the smart card public telephone in France and Germany. Telephone cards incorporating chips are currently used in more than 50 countries.

The integrated circuits used in telephone cards are relatively small, simple and inexpensive memory chips with specific security logic that allows the card balance to be reduced while protecting it against manipulation. Microprocessor chips, which are significantly larger and more complex, were first used in large numbers in telecommunications applications, specifically for mobile telecommunications. **In 1988, the German Post Office acted as a pioneer in this area by introducing a modern microprocessor card using EEPROM technology as an authorization card for the analog mobile telephone network (C-Netz).** The reason for introducing such cards was an increasing incidence of fraud with the magnetic-stripe cards used up to that time. For technical reasons, the analog mobile telephone network was limited to a relatively small number of subscribers (around one million), so it was not a true mass market for microprocessor cards. **However, the positive experience gained from using smart cards in the analog mobile telephone system was decisive for the introduction of smart cards into the digital GSM network.** This network was put into service in 1991 in various European countries and has presently expanded over the entire world, with over 600 million subscribers in more than 170 countries.

Progress was significantly slower in the field of bank cards, in part due to their greater complexity compared with telephone cards. Here we would just like to remark that the development of **modern cryptography** has been just as crucial for the proliferation of bank cards as developments in semiconductor technology.

With the general expansion of electronic data processing in the 1960s, the discipline of cryptography experienced a sort of quantum leap. Modern hardware and software made it possible to implement complex, sophisticated mathematical algorithms that allowed previously unparalleled levels of security to be achieved. Moreover, this new technology was available to everyone, in contrast to the previous situation in which cryptography was a covert science in the private reserve of the military and secret services. With these modern cryptographic procedures, the strength of the security mechanisms in electronic data-processing systems could be mathematically calculated. It was no longer necessary to rely on a highly subjective assessment of conventional techniques, whose security essentially rests on the secrecy of the procedures used.

The smart card proved to be an ideal medium. It made a high level of security (based on cryptography) available to everyone, since it could safely store secret keys and execute cryptographic algorithms. In addition, smart cards are so small and easy to handle that they can be carried and used everywhere by everybody in everyday life. It was a natural idea to attempt to use these new security features for bank cards, in order to come to grips with the security risks arising from the increasing use of magnetic-stripe cards.

**The French banks were the first to introduce this fascinating technology in 1984, following a trial with 60,000 cards in 1982–83.** It took another 10 years before all French bank cards incorporated chips. In Germany, the first field trials took place in 1984–85, using a multifunctional payment card incorporating a chip. However, the Zentrale Kreditausschuss (ZKA), which is the coordinating committee of the leading German banks, did not manage to issue a specification for multifunctional Eurocheque cards incorporating chips until 1996. **In 1997, all German savings associations and many banks issued the new smart cards. In the previous year, multifunctional smart cards with POS functions, an electronic purse and optional value-added services were issued in all of Austria. This made Austria the first country in the world to have a nationwide electronic purse system.**

An important milestone for the future worldwide use of smart cards for making payments was the completion of the **EMV specification**, which was a product of the joint efforts of **Europay**, **MasterCard** and **Visa**. The first version of this specification was published in 1994. It contained detailed descriptions of credit cards incorporating microprocessor chips, and it guaranteed the mutual compatibility of the future smart cards of the three largest credit card organizations.

**Electronic purse systems have proven to be another major factor in promoting the international use of smart cards for financial transactions. The first such system, called Danmont, was put into operation in Denmark in 1992.** There are currently more than 20 national systems in use in Europe alone, many of which are based on the European EN 1546 standard. The use of such systems is also increasing outside of Europe. In the USA, where smart-card systems have had a hard time becoming stablished, Visa experimented with a smart-card purse during the 1996 Olympic Summer Games in Atlanta. **Payments via the Internet offer a new and promising application area for electronic purses.** However, the problems associated with making small payments securely but anonymously throughout the world via the public Internet have not
yet been solved in a satisfactory manner. Smart cards could play a decisive role in providing an answer to these problems. Besides this, smart cards could plan an important role in introducing **electronic signatures**. Several European countries have initiated the introduction of electronic signature systems after a legal basis for the use of electronic signatures was provided by approval of a European directive regarding electronic signatures in 1999.

As the result of another application, almost every German citizen now possesses a smart card. When **health insurance cards** incorporating chips were introduced, more than 70 million smart cards were issued to all persons enrolled in the national health insurance plan. Presently, smart cards are being used in the health-care sector in many countries.

The smart card's high degree of functional flexibility, which even allows programs for new applications to be added to a card already in use, has opened up completely new application areas extending beyond the boundaries of traditional card uses. Smart cards are also being used as 'electronic tickets' for local public transport in many cities throughout the world. **Contactless smart cards** are usually used for such applications, since they are particularly convenient and user friendly.


# Application Areas

## Memory Cards

The first smart cards used in large quantities were memory cards for telephone applications. These cards are **prepaid**, with the value stored electronically in the chip being decreased by the amount of the call charge each time the card is used.

Naturally, it is necessary to prevent the user from subsequently increasing the stored value, which could easily be done with a magnetic-stripe card. With such a card, all the user would have to do is record the data stored at the time of purchase and rewrite them to the magnetic stripe after using the card. The card would then have its original value and could be reused. This type of manipulation, known as **buffering**, is prevented in smart phone cards by security logic in the chip that makes it
impossible to erase a memory cell once it has been written. The reduction of the card balance by the number of charge units used is thus irreversible.

This type of smart card can naturally be used not only for telephone calls, but also whenever goods or services are to be sold against prior payment without the use of cash. Examples of possible uses include local public transport, vending machines of all types, cafeterias, swimming pools, car parks and so on. The advantage of this type of card lies in its simple technology (the surface area of the chip is typically only a few square millimeters), and hence its low cost. The disadvantage is that the card cannot be reused once it is empty, but must be discarded as waste – unless it ends up in a card collection.

Another typical application of memory cards is the German health insurance card, which has been issued since 1994 to all persons enrolled in the national health insurance plan. The information previously written on the patient’s card is now stored in the chip and printed or laser-engraved on the card. Using a chip for data storage makes the cards machine-readable using simple equipment.

In summary, memory-type smart cards have limited functionality. Their integrated security logic makes it possible to protect stored data against manipulation. They are suitable for use as prepaid cards or identification cards in systems where low cost is a primary consideration.

## Microprocessor cards

As already noted, microprocessor cards were first used in the form of bank cards in France. Their ability to securely store private keys and execute modern cryptographic algorithms made it possible to implement highly secure offline payment systems.

Since the microprocessor built into the card is freely programmable, the functionality of microprocessor cards is restricted only by the available storage space and the capacity of the processor. The only limits to the designer's imagination when implementing smart card systems are thus technological, and they are extended enormously with each new generation of integrated circuits.

Possible applications for microprocessor cards include identification, access control systems for restricted areas and computers, secure data storage, electronic signatures and electronic purses, as well as multifunctional cards incorporating several applications in a single card. Modern smart-card operating systems also allow new applications to be loaded into a card after it has already been issued to the user, without compromising the security of the various applications.

This new flexibility opens up completely new application areas. For example, personal security modules are indispensable if Internet commerce and payments are to be made trustworthy. Such security modules could securely store personal keys and execute high-performance cryptographic algorithms. These tasks can be performed in an elegant manner by a microprocessor with a cryptographic coprocessor. Specifications for secure Internet applications using smart cards are currently being developed throughout the world. Within a few years, we can expect to see every PC equipped with a smart-card interface.

In summary, the essential advantages of microprocessor cards are large storage capacity, the ability to securely store confidential data and the ability to execute cryptographic algorithms. These advantages make a wide range of new applications possible, in addition to the traditional bank card application. The potential of smart cards is by no means yet exhausted, and furthermore, it is constantly being expanded by progress in semiconductor technology.

## Contactless Cards

Contactless cards, in which energy and data are transferred without any electrical contact between the card and the terminal, have achieved the status of commercial products in the last few years. Presently, both memory cards and microprocessor cards are available as contactless cards. Although contactless microprocessor cards can usually work at a distance of only a few centimeters from the terminal, contactless memory cards can be used up to a meter away from the terminal. This means that such cards do not necessarily have to be held in the user’s hand during use, but can remain in the user's purse or wallet.

Contactless cards are thus particularly suitable for applications in which persons or objects should be quickly identified. Sample applications are:

- access control,
- local public transportation,
- ski passes,
- airline tickets,
- baggage identification.

However, there are also applications where operation over a long distance could cause problems and should thus be prevented. A typical example is an electronic purse. A declaration of intent on the part of the cardholder is normally required to complete a financial transaction. This confirms the amount of the payment and the cardholder’s agreement to pay. With a contactless card, this declaration takes the form of inserting the card in the terminal and confirming the indicated amount using the keypad. If contactless payments over relatively long distances were possible, a ‘con artist’ could remove money from the electronic purse without the knowledge of the cardholder. Dual-interface cards (sometimes called ‘combicards’) offer a possible solution to this problem. These cards combine contact and contactless interfaces in a single card. Such a card can communicate with the terminal via either its contact interface or its contactless interface, according to what is desired.

There is great interest in contactless cards in the field of local public transportation. If the smart cards presently used in payment systems, which are generally contact-type cards, can have their functionality extended to include acting as electronic tickets with contactless interfaces, transportation operators could use the existing infrastructure and cards of the credit card industry.

# Standardization



# Payment types

- Eletronic purse systems  
- Payment via the Internet  


# References  

- RANKL, W., EFFING, W. Smart Card Handbook. 4th edition. John Wiley & Sons Ltd, 2010.  
