

The end product from a digital signature process is a **PAdES** \(PDF Advanced Electronic Signature\). This is a standardized PDF-format which contains key information about the signature, such as a time-stamp and details about the eID method used to sign \(i.e. BankID\).

Signature data is incorporated directly within the signed PDF document, much as an ink signature becomes an integral part of a paper document, allowing the complete self-contained PDF file to be copied, stored and distributed as a simple electronic file. The document can be validated by a third party to ensure that the document has not been faked or tampered with. Our validation API can be used to validate signed documents. 

A significant advantage of PAdES is that it is being deployed by means of widely available PDF software: it does not require development or customization of specialized software. When opening a PAdES in for instance Acrobat Reader, a blue line will appear in the top of the document. This blue line indicates that the document integrity is intact and that the document has not been changed or tampered with after the time of signature. 



