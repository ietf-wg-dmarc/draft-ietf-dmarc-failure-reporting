Internet-Draft

DMARC Failure Reporting

February 2021

Jones & Vesely

Expires 5 August 2021

\[Page\]

<div id="external-metadata" class="document-information">

</div>

<div id="internal-metadata" class="document-information">

  - Workgroup:  
    DMARC Working Group

  - Internet-Draft:  
    draft-ietf-dmarc-failure-reporting-01

  - Obsoletes:  
    [7489](https://www.rfc-editor.org/rfc/rfc7489) (if approved)

  - Published:  
    1 February 2021

  - Intended Status:  
    Standards Track

  - Expires:  
    5 August 2021

  - Authors:
    
    <div class="author">
    
    <div class="author-name">
    
    S. M. Jones, <span class="editor">Ed.</span>
    
    </div>
    
    <div class="org">
    
    DMARC.org
    
    </div>
    
    </div>
    
    <div class="author">
    
    <div class="author-name">
    
    A. Vesely,
<span class="editor">Ed.</span>
    
    </div>
    
    <div class="org">
    
    Tana
    
    </div>
    
    </div>

</div>

# Domain-based Message Authentication, Reporting, and Conformance (DMARC) Failure Reporting

<div id="section-abstract" class="section">

## [Abstract](#abstract)

Domain-based Message Authentication, Reporting, and Conformance (DMARC)
is a scalable mechanism by which a domain owner can request feedback
about email messages using their domain in the From: address field. This
document describes "failure reports," or "failed message reports," which
provide details about individual messages that failed to authenticate
according to the DMARC mechanism.[¶](#section-abstract-1)

</div>

<div id="status-of-memo">

<div id="section-boilerplate.1" class="section">

## [Status of This Memo](#name-status-of-this-memo)

This Internet-Draft is submitted in full conformance with the provisions
of BCP 78 and BCP 79.[¶](#section-boilerplate.1-1)

Internet-Drafts are working documents of the Internet Engineering Task
Force (IETF). Note that other groups may also distribute working
documents as Internet-Drafts. The list of current Internet-Drafts is at
<span><https://datatracker.ietf.org/drafts/current/></span>.[¶](#section-boilerplate.1-2)

Internet-Drafts are draft documents valid for a maximum of six months
and may be updated, replaced, or obsoleted by other documents at any
time. It is inappropriate to use Internet-Drafts as reference material
or to cite them other than as "work in
progress."[¶](#section-boilerplate.1-3)

This Internet-Draft will expire on 5 August
2021.[¶](#section-boilerplate.1-4)

</div>

</div>

<div id="copyright">

<div id="section-boilerplate.2" class="section">

## [Copyright Notice](#name-copyright-notice)

Copyright (c) 2021 IETF Trust and the persons identified as the document
authors. All rights reserved.[¶](#section-boilerplate.2-1)

This document is subject to BCP 78 and the IETF Trust's Legal Provisions
Relating to IETF Documents
(<span><https://trustee.ietf.org/license-info></span>) in effect on the
date of publication of this document. Please review these documents
carefully, as they describe your rights and restrictions with respect to
this document. Code Components extracted from this document must include
Simplified BSD License text as described in Section 4.e of the Trust
Legal Provisions and are provided without warranty as described in the
Simplified BSD
    License.[¶](#section-boilerplate.2-2)

</div>

</div>

<div id="toc">

<div id="section-toc.1" class="section">

[▲](#)

## [Table of Contents](#name-table-of-contents)

  - 
    
    <div id="section-toc.1-1.1">
    
    [1](#section-1).  [Introduction](#name-introduction)[¶](#section-toc.1-1.1.1)
    
    </div>

  - 
    
    <div id="section-toc.1-1.2">
    
    [2](#section-2).  [Terminology and
    Definitions](#name-terminology-and-definitions)[¶](#section-toc.1-1.2.1)
    
    </div>

  - 
    
    <div id="section-toc.1-1.3">
    
    [3](#section-3).  [Failure
    Reports](#name-failure-reports)[¶](#section-toc.1-1.3.1)
    
      - 
        
        <div id="section-toc.1-1.3.2.1">
        
        [3.1](#section-3.1).  [Reporting Format
        Update](#name-reporting-format-update)[¶](#section-toc.1-1.3.2.1.1)
        
        </div>
    
      - 
        
        <div id="section-toc.1-1.3.2.2">
        
        [3.2](#section-3.2).  [Verifying External
        Destinations](#name-verifying-external-destinat)[¶](#section-toc.1-1.3.2.2.1)
        
        </div>
    
      - 
        
        <div id="section-toc.1-1.3.2.3">
        
        [3.3](#section-3.3).  [Transport](#name-transport)[¶](#section-toc.1-1.3.2.3.1)
        
        </div>
    
    </div>

  - 
    
    <div id="section-toc.1-1.4">
    
    [4](#section-4).  [Privacy
    Considerations](#name-privacy-considerations)[¶](#section-toc.1-1.4.1)
    
      - 
        
        <div id="section-toc.1-1.4.2.1">
        
        [4.1](#section-4.1).  [Data Exposure
        Considerations](#name-data-exposure-consideration)[¶](#section-toc.1-1.4.2.1.1)
        
        </div>
    
      - 
        
        <div id="section-toc.1-1.4.2.2">
        
        [4.2](#section-4.2).  [Report
        Recipients](#name-report-recipients)[¶](#section-toc.1-1.4.2.2.1)
        
        </div>
    
    </div>

  - 
    
    <div id="section-toc.1-1.5">
    
    [5](#section-5).  [Security
    Considerations](#name-security-considerations)[¶](#section-toc.1-1.5.1)
    
    </div>

  - 
    
    <div id="section-toc.1-1.6">
    
    [6](#section-6).  [Normative
    References](#name-normative-references)[¶](#section-toc.1-1.6.1)
    
    </div>

  - 
    
    <div id="section-toc.1-1.7">
    
    [7](#section-7).  [Informative
    References](#name-informative-references)[¶](#section-toc.1-1.7.1)
    
    </div>

  - 
    
    <div id="section-toc.1-1.8">
    
    [Appendix
    A](#section-appendix.a).  [Examples](#name-examples)[¶](#section-toc.1-1.8.1)
    
      - 
        
        <div id="section-toc.1-1.8.2.1">
        
        [A.1](#section-a.1).  [Entire Domain, Monitoring Only,
        Per-Message
        Reports](#name-entire-domain-monitoring-on)[¶](#section-toc.1-1.8.2.1.1)
        
        </div>
    
      - 
        
        <div id="section-toc.1-1.8.2.2">
        
        [A.2](#section-a.2).  [Per-Message Failure Reports Directed to
        Third
        Party](#name-per-message-failure-reports)[¶](#section-toc.1-1.8.2.2.1)
        
        </div>
    
    </div>

  - 
    
    <div id="section-toc.1-1.9">
    
    [Appendix B](#section-appendix.b).  [Change
    Log](#name-change-log)[¶](#section-toc.1-1.9.1)
    
    </div>

  - 
    
    <div id="section-toc.1-1.10">
    
    [](#section-appendix.c)[Acknowledgements](#name-acknowledgements)[¶](#section-toc.1-1.10.1)
    
    </div>

  - 
    
    <div id="section-toc.1-1.11">
    
    [](#section-appendix.d)[Authors'
    Addresses](#name-authors-addresses)[¶](#section-toc.1-1.11.1)
    
    </div>

</div>

</div>

<div id="introduction">

<div id="section-1" class="section">

## [1.](#section-1)[Introduction](#name-introduction)

Domain-based Message Authentication, Reporting, and Conformance (DMARC)
<span>\[[I-D.ietf-dmarc-dmarcbis](#I-D.ietf-dmarc-dmarcbis)\]</span> is
a scalable mechanism by which a mail-originating organization can
express domain-level policies and preferences for message validation,
disposition, and reporting, that a mail-receiving organization can use
to improve mail handling. This document focuses on one type of reporting
that can be requested under DMARC.[¶](#section-1-1)

Failure reports provide detailed information about the failure of a
single message or a group of similar messages failing for the same
reason. They are meant to aid in cases where a domain owner is unable to
detect why failures reported in aggregate form did occur. It is
important to note these reports can contain either the header or the
entire content of a failed message, which in turn may contain personally
identifiable information, which should be considered when deciding
whether to generate such
reports.[¶](#section-1-2)

</div>

</div>

<div id="terminology">

<div id="section-2" class="section">

## [2.](#section-2)[Terminology and Definitions](#name-terminology-and-definitions)

This section defines terms used in the rest of the
document.[¶](#section-2-1)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
"OPTIONAL" in this document are to be interpreted as described in BCP 14
<span>\[[RFC2119](#RFC2119)\]</span>
<span>\[[RFC8174](#RFC8174)\]</span> when, and only when, they appear in
all capitals, as shown here.[¶](#section-2-2)

Readers are expected to be familiar with the contents of
<span>\[[I-D.ietf-dmarc-dmarcbis](#I-D.ietf-dmarc-dmarcbis)\]</span>,
specifically the terminology and definitions section.[¶](#section-2-3)

</div>

</div>

<div id="failure-reports">

<div id="section-3" class="section">

## [3.](#section-3)[Failure Reports](#name-failure-reports)

Failure reports can supply more detailed information about messages that
failed to authenticate, enabling the Domain Owner to determine exactly
what might be causing those specific failures.[¶](#section-3-1)

Failure reports are normally generated and sent almost immediately after
the Mail Receiver detects a DMARC failure. Rather than waiting for an
aggregate report, these reports are useful for quickly notifying the
Domain Owners when there is an authentication failure. Whether the
failure is due to an infrastructure problem or the message is
inauthentic, failure reports also provide more information about the
failed message than is available in an aggregate
report.[¶](#section-3-2)

These reports should include as much of the message header and body as
possible, consistent with the reporting party's privacy policies, to
enable the Domain Owner to diagnose the authentication
failure.[¶](#section-3-3)

When a Domain Owner requests failure reports for the purpose of forensic
analysis, and the Mail Receiver is willing to provide such reports, the
Mail Receiver generates and sends a message using the format described
in <span>\[[RFC6591](#RFC6591)\]</span>; this document updates that
reporting format, as described in [Section
3.1](#reporting-format-update).[¶](#section-3-4)

The destination(s) and nature of the reports are defined by the "ruf"
and "fo" tags as defined in
<span>[Section 6.3](https://tools.ietf.org/html/draft-ietf-dmarc-dmarcbis-00#section-6.3)
of
\[[I-D.ietf-dmarc-dmarcbis](#I-D.ietf-dmarc-dmarcbis)\]</span>.[¶](#section-3-5)

Where multiple URIs are selected to receive failure reports, the report
generator MUST make an attempt to deliver to each of
them.[¶](#section-3-6)

An obvious consideration is the denial-of-service attack that can be
perpetrated by an attacker who sends numerous messages purporting to be
from the intended victim Domain Owner but that fail both SPF and DKIM;
this would cause participating Mail Receivers to send failure reports to
the Domain Owner or its delegate in potentially huge volumes.
Accordingly, participating Mail Receivers are encouraged to aggregate
these reports as much as is practical, using the Incidents field of the
Abuse Reporting Format (<span>\[[RFC5965](#RFC5965)\]</span>). Various
aggregation techniques are possible, including the
following:[¶](#section-3-7)

  - 
    
    <div id="section-3-8.1">
    
    only send a report to the first recipient of multi-recipient
    messages;[¶](#section-3-8.1.1)
    
    </div>

  - 
    
    <div id="section-3-8.2">
    
    store reports for a period of time before sending them, allowing
    detection, collection, and reporting of like
    incidents;[¶](#section-3-8.2.1)
    
    </div>

  - 
    
    <div id="section-3-8.3">
    
    apply rate limiting, such as a maximum number of reports per minute
    that will be generated (and the remainder
    discarded).[¶](#section-3-8.3.1)
    
    </div>

<div id="reporting-format-update">

<div id="section-3.1" class="section">

### [3.1.](#section-3.1)[Reporting Format Update](#name-reporting-format-update)

Operators implementing this specification also implement an augmented
version of <span>\[[RFC6591](#RFC6591)\]</span> as
follows:[¶](#section-3.1-1)

1.  
    
    <div id="section-3.1-2.1">
    
    A DMARC failure report includes the following ARF header fields,
    with the indicated normative requirement
    levels:[¶](#section-3.1-2.1.1)
    
      - 
        
        <div id="section-3.1-2.1.2.1">
        
        Identity-Alignment (REQUIRED; defined
        below)[¶](#section-3.1-2.1.2.1.1)
        
        </div>
    
      - 
        
        <div id="section-3.1-2.1.2.2">
        
        Delivery-Result (OPTIONAL)[¶](#section-3.1-2.1.2.2.1)
        
        </div>
    
      - 
        
        <div id="section-3.1-2.1.2.3">
        
        DKIM-Domain, DKIM-Identity, DKIM-Selector (REQUIRED if the
        message was signed by DKIM)[¶](#section-3.1-2.1.2.3.1)
        
        </div>
    
      - 
        
        <div id="section-3.1-2.1.2.4">
        
        DKIM-Canonicalized-Header, DKIM-Canonicalized-Body (OPTIONAL if
        the message was signed by DKIM)[¶](#section-3.1-2.1.2.4.1)
        
        </div>
    
      - 
        
        <div id="section-3.1-2.1.2.5">
        
        SPF-DNS (REQUIRED)[¶](#section-3.1-2.1.2.5.1)
        
        </div>
    
    </div>

2.  
    
    <div id="section-3.1-2.2">
    
    The "Identity-Alignment" field is defined to contain a comma-
    separated list of authentication mechanism names that produced an
    aligned identity, or the keyword "none" if none did.
    ABNF:[¶](#section-3.1-2.2.1)
    
    </div>

<div id="section-3.1-3" class="artwork art-text alignLeft">

``` 
  id-align     = "Identity-Alignment:" [CFWS]
                 ( "none" /
                   dmarc-method *( [CFWS] "," [CFWS] dmarc-method ) )
                 [CFWS]

  dmarc-method = ( "dkim" / "spf" )
                 ; each may appear at most once in an id-align
```

[¶](#section-3.1-3)

</div>

3.  <span id="section-3.1-4.1">Authentication Failure Type "dmarc" is
    defined, which is to be used when a failure report is generated
    because some or all of the authentication mechanisms failed to
    produce aligned identifiers. Note that a failure report generator
    MAY also independently produce an AFRF message for any or all of the
    underlying authentication
methods.[¶](#section-3.1-4.1)</span>

</div>

</div>

<div id="verifying-external-destinations">

<div id="section-3.2" class="section">

### [3.2.](#section-3.2)[Verifying External Destinations](#name-verifying-external-destinat)

The procedure described for aggragate reports
<span>[Section 2.1](https://tools.ietf.org/html/draft-ietf-dmarc-aggregate-reporting-00#section-2.1)
of
\[[I-D.ietf-dmarc-aggregate-reporting](#I-D.ietf-dmarc-aggregate-reporting)\]</span>
applies to failure reports as well.[¶](#section-3.2-1)

</div>

</div>

<div id="transport">

<div id="section-3.3" class="section">

### [3.3.](#section-3.3)[Transport](#name-transport)

Email streams carrying DMARC failure reports SHOULD provide DMARC-based
authentication, so as to produce "dmarc=pass". This requirement is a
MUST in case the report is sent through a host having a DMARC record
with a ruf= tag. Indeed, special care must be taken of authentication in
that case, as failure to authenticate failure reports may result in mail
loops.[¶](#section-3.3-1)

Reporters SHOULD rate limit the number of failure reports sent to any
recipient to avoid overloading recipient systems. Again, in case the
reports being sent are in turn at risk of being reported for DMARC
authentication failure, reporters MUST make sure that possible mail loop
are
stopped.[¶](#section-3.3-2)

</div>

</div>

</div>

</div>

<div id="privacy-considerations">

<div id="section-4" class="section">

## [4.](#section-4)[Privacy Considerations](#name-privacy-considerations)

This section discusses issues specific to private data that may be
included in the DMARC reporting
functions.[¶](#section-4-1)

<div id="data-exposure-considerations">

<div id="section-4.1" class="section">

### [4.1.](#section-4.1)[Data Exposure Considerations](#name-data-exposure-consideration)

Failed-message reporting provides message-specific details pertaining to
authentication failures. Individual reports can contain message content
as well as trace header fields. Domain Owners are able to analyze
individual reports and attempt to determine root causes of
authentication mechanism failures, gain insight into misconfigurations
or other problems with email and network infrastructure, or inspect
messages for insight into abusive practices.[¶](#section-4.1-1)

These reports may expose sender and recipient identifiers (e.g.,
RFC5322.From addresses), and although the
<span>\[[RFC6591](#RFC6591)\]</span> format used for failed-message
reporting supports redaction, failed-message reporting is capable of
exposing the entire message to the report recipient.[¶](#section-4.1-2)

Domain Owners requesting reports will receive information about mail
claiming to be from them, which includes mail that was not, in fact,
from them. Information about the final destination of mail where it
might otherwise be obscured by intermediate systems will therefore be
exposed.[¶](#section-4.1-3)

When message-forwarding arrangements exist, Domain Owners requesting
reports will also receive information about mail forwarded to domains
that were not originally part of their messages' recipient lists. This
means that destination domains previously unknown to the Domain Owner
may now become visible.[¶](#section-4.1-4)

Disclosure of information about the messages is being requested by the
entity generating the email in the first place, i.e., the Domain Owner
and not the Mail Receiver, so this may not fit squarely within existing
privacy policy provisions. For some providers, failed-message reporting
is viewed as a function similar to complaint reporting about spamming or
phishing and is treated similarly under the privacy policy. Report
generators (i.e., Mail Receivers) are encouraged to review their
reporting limitations under such policies before enabling DMARC
reporting.[¶](#section-4.1-5)

</div>

</div>

<div id="report-recipients">

<div id="section-4.2" class="section">

### [4.2.](#section-4.2)[Report Recipients](#name-report-recipients)

A DMARC record can specify that reports should be sent to an
intermediary operating on behalf of the Domain Owner. This is done when
the Domain Owner contracts with an entity to monitor mail streams for
abuse and performance issues. Receipt by third parties of such data may
or may not be permitted by the Mail Receiver's privacy policy, terms of
use, or other similar governing document. Domain Owners and Mail
Receivers should both review and understand if their own internal
policies constrain the use and transmission of DMARC
reporting.[¶](#section-4.2-1)

Some potential exists for report recipients to perform traffic analysis,
making it possible to obtain metadata about the Receiver's traffic. In
addition to verifying compliance with policies, Receivers need to
consider that before sending reports to a third
party.[¶](#section-4.2-2)

</div>

</div>

</div>

</div>

<div id="security-considerations">

<div id="section-5" class="section">

## [5.](#section-5)[Security Considerations](#name-security-considerations)

Considerations discussed in
<span>[Section 11](https://tools.ietf.org/html/draft-ietf-dmarc-dmarcbis-00#section-11)
of \[[I-D.ietf-dmarc-dmarcbis](#I-D.ietf-dmarc-dmarcbis)\]</span>
apply.[¶](#section-5-1)

In addition, note that Organizational Domains are only an approximation
to actual domain ownership. Therefore, reports may be sent to someone
unrelated to the actual sender or domain owner. That makes
considerations in [Section 4.1](#data-exposure-considerations) all the
more relevant.[¶](#section-5-2)

</div>

</div>

<div id="section-6" class="section">

## [6.](#section-6)[Normative References](#name-normative-references)

  - \[RFC2119\]  
    <span class="refAuthor">Bradner, S.</span>,
    <span class="refTitle">"Key words for use in RFCs to Indicate
    Requirement Levels"</span>, <span class="seriesInfo">BCP 14</span>,
    <span class="seriesInfo">RFC 2119</span>,
    <span class="seriesInfo">DOI 10.17487/RFC2119</span>, March 1997,
    <span>\<<https://www.rfc-editor.org/info/rfc2119>\></span>.
  - \[RFC6591\]  
    <span class="refAuthor">Fontana, H.</span>,
    <span class="refTitle">"Authentication Failure Reporting Using the
    Abuse Reporting Format"</span>, <span class="seriesInfo">RFC
    6591</span>, <span class="seriesInfo">DOI 10.17487/RFC6591</span>,
    April 2012,
    <span>\<<https://www.rfc-editor.org/info/rfc6591>\></span>.
  - \[I-D.ietf-dmarc-dmarcbis\]  
    <span class="refAuthor">Gustafsson,
    E.</span><span class="refAuthor">, Herr,
    T.</span><span class="refAuthor">, and J. Levine</span>,
    <span class="refTitle">"Domain-based Message Authentication,
    Reporting, and Conformance (DMARC)"</span>,
    <span class="refContent">Work in Progress</span>,
    <span class="seriesInfo">Internet-Draft,
    draft-ietf-dmarc-dmarcbis-00</span>, 11 November 2020,
    <span>\<<https://tools.ietf.org/html/draft-ietf-dmarc-dmarcbis-00>\></span>.
  - \[I-D.ietf-dmarc-aggregate-reporting\]  
    <span class="refAuthor">Brotman, A.</span>,
    <span class="refTitle">"DMARC Aggregate Reporting"</span>,
    <span class="refContent">Work in Progress</span>,
    <span class="seriesInfo">Internet-Draft,
    draft-ietf-dmarc-aggregate-reporting-00</span>, 12 November 2020,
    <span>\<<https://tools.ietf.org/html/draft-ietf-dmarc-aggregate-reporting-00>\></span>.

</div>

<div id="section-7" class="section">

## [7.](#section-7)[Informative References](#name-informative-references)

  - \[RFC5965\]  
    <span class="refAuthor">Shafranovich,
    Y.</span><span class="refAuthor">, Levine,
    J.</span><span class="refAuthor">, and M. Kucherawy</span>,
    <span class="refTitle">"An Extensible Format for Email Feedback
    Reports"</span>, <span class="seriesInfo">RFC 5965</span>,
    <span class="seriesInfo">DOI 10.17487/RFC5965</span>, August 2010,
    <span>\<<https://www.rfc-editor.org/info/rfc5965>\></span>.
  - \[RFC8174\]  
    <span class="refAuthor">Leiba, B.</span>,
    <span class="refTitle">"Ambiguity of Uppercase vs Lowercase in RFC
    2119 Key Words"</span>, <span class="seriesInfo">BCP 14</span>,
    <span class="seriesInfo">RFC 8174</span>,
    <span class="seriesInfo">DOI 10.17487/RFC8174</span>, May 2017,
    <span>\<<https://www.rfc-editor.org/info/rfc8174>\></span>.

</div>

<div id="examples">

<div id="section-appendix.a" class="section">

## [Appendix A.](#section-appendix.a)[Examples](#name-examples)

This section presents some examples related to the use of DMARC
reporting
functions.[¶](#section-appendix.a-1)

<div id="entire-domain-monitoring-only-per-message-reports">

<div id="section-a.1" class="section">

## [A.1.](#section-a.1)[Entire Domain, Monitoring Only, Per-Message Reports](#name-entire-domain-monitoring-on)

The owners of the domain "example.com" have deployed SPF and DKIM on
their messaging infrastructure. As described in, <span>[Appendix
B.2.1](https://tools.ietf.org/html/draft-ietf-dmarc-aggregate-reporting-00#appendix-B.2.1)
of
\[[I-D.ietf-dmarc-aggregate-reporting](#I-D.ietf-dmarc-aggregate-reporting)\]</span>
they have used the aggregate reporting to discover some messaging
systems that had not yet implemented DKIM correctly. However, they are
still seeing periodic authentication failures. In order to diagnose
these intermittent problems, they wish to request per-message failure
reports when authentication failures occur.[¶](#section-a.1-1)

Not all Receivers will honor such a request, but the Domain Owner feels
that any reports it does receive will be helpful enough to justify
publishing this record. The default per-message report format
(<span>\[[RFC6591](#RFC6591)\]</span>) meets the Domain Owner's needs in
this scenario.[¶](#section-a.1-2)

The Domain Owner accomplishes this by adding the following to its policy
record:[¶](#section-a.1-3)

  - <span id="section-a.1-4.1">Per-message failure reports should be
    sent via email to the address "auth-reports@example.com"
    ("ruf=mailto:auth-reports@example.com")[¶](#section-a.1-4.1)</span>

The updated DMARC policy record might look like this when retrieved
using a common command-line tool (the output shown would appear on a
single line but is wrapped here for publication):[¶](#section-a.1-5)

<div id="section-a.1-6" class="artwork art-text alignLeft">

``` 
  % dig +short TXT _dmarc.example.com.
  "v=DMARC1; p=none; rua=mailto:dmarc-feedback@example.com;
   ruf=mailto:auth-reports@example.com"
```

[¶](#section-a.1-6)

</div>

To publish such a record, the DNS administrator for the Domain Owner
might create an entry like the following in the appropriate zone file
(following the conventional zone file format):[¶](#section-a.1-7)

<div id="section-a.1-8" class="artwork art-text alignLeft">

``` 
  ; DMARC record for the domain example.com

  _dmarc  IN TXT ( "v=DMARC1; p=none; "
                    "rua=mailto:dmarc-feedback@example.com; "
                    "ruf=mailto:auth-reports@example.com" )
```

[¶](#section-a.1-8)

</div>

</div>

</div>

<div id="per-message-failure-reports-directed-to-third-party">

<div id="section-a.2" class="section">

## [A.2.](#section-a.2)[Per-Message Failure Reports Directed to Third Party](#name-per-message-failure-reports)

The Domain Owner from the previous example is maintaining the same
policy but now wishes to have a third party receive and process the
per-message failure reports. Again, not all Receivers will honor this
request, but those that do may implement additional checks to validate
that the third party wishes to receive the failure reports for this
domain.[¶](#section-a.2-1)

The Domain Owner needs to alter its policy record from [Appendix
A.1](#entire-domain-monitoring-only-per-message-reports) as
follows:[¶](#section-a.2-2)

  - <span id="section-a.2-3.1">Per-message failure reports should be
    sent via email to the address "auth-reports@thirdparty.example.net"
    ("ruf=mailto:auth-reports@thirdparty.example.net")[¶](#section-a.2-3.1)</span>

The DMARC policy record might look like this when retrieved using a
common command-line tool (the output shown would appear on a single line
but is wrapped here for publication):[¶](#section-a.2-4)

<div id="section-a.2-5" class="artwork art-text alignLeft">

``` 
  % dig +short TXT _dmarc.example.com.
  "v=DMARC1; p=none; rua=mailto:dmarc-feedback@example.com;
   ruf=mailto:auth-reports@thirdparty.example.net"
```

[¶](#section-a.2-5)

</div>

To publish such a record, the DNS administrator for the Domain Owner
might create an entry like the following in the appropriate zone file
(following the conventional zone file format):[¶](#section-a.2-6)

<div id="section-a.2-7" class="artwork art-text alignLeft">

``` 
  ; DMARC record for the domain example.com

  _dmarc IN TXT ( "v=DMARC1; p=none; "
                  "rua=mailto:dmarc-feedback@example.com; "
                  "ruf=mailto:auth-reports@thirdparty.example.net" )
```

[¶](#section-a.2-7)

</div>

Because the address used in the "ruf" tag is outside the Organizational
Domain in which this record is published, conforming Receivers will
implement additional checks as described in [Section
3.2](#verifying-external-destinations) of this document. In order to
pass these additional checks, the third party will need to publish an
additional DNS record as follows:[¶](#section-a.2-8)

  - <span id="section-a.2-9.1">Given the DMARC record published by the
    Domain Owner at "\_dmarc.example.com", the DNS administrator for the
    third party will need to publish a TXT resource record at
    "example.com.\_report.\_dmarc.thirdparty.example.net" with the value
    "v=DMARC1;".[¶](#section-a.2-9.1)</span>

The resulting DNS record might look like this when retrieved using a
common command-line tool (the output shown would appear on a single line
but is wrapped here for publication):[¶](#section-a.2-10)

<div id="section-a.2-11" class="artwork art-text alignLeft">

``` 
  % dig +short TXT example.com._report._dmarc.thirdparty.example.net
  "v=DMARC1;"
```

[¶](#section-a.2-11)

</div>

To publish such a record, the DNS administrator for example.net might
create an entry like the following in the appropriate zone file
(following the conventional zone file format):[¶](#section-a.2-12)

<div id="section-a.2-13" class="artwork art-text alignLeft">

``` 
  ; zone file for thirdparty.example.net
  ; Accept DMARC failure reports on behalf of example.com

  example.com._report._dmarc   IN   TXT    "v=DMARC1;"
```

[¶](#section-a.2-13)

</div>

Intermediaries and other third parties should refer to [Section
3.2](#verifying-external-destinations) for the full details of this
mechanism.[¶](#section-a.2-14)

</div>

</div>

</div>

</div>

<div id="change-log">

<div id="section-appendix.b" class="section">

## [Appendix B.](#section-appendix.b)[Change Log](#name-change-log)

\[RFC Editor: Please remove this section prior to
publication.\][¶](#section-appendix.b-1)

<span class="break"></span>

  - 00 to 01
    
      - <span id="section-appendix.b-2.2.1.1">Replace references to
        RFC7489 with references to
        I-D.ietf-dmarc-dmarcbis.[¶](#section-appendix.b-2.2.1.1)</span>
      - <span id="section-appendix.b-2.2.1.2">Replace the 2nd paragraph
        in the Introduction with the text proposed by Ned for Ticket
        \#55, which enjoys some
        consensus:  
        https://mailarchive.ietf.org/arch/msg/dmarc/HptVyJ9SgrfxWRbeGwORagPrhCw[¶](#section-appendix.b-2.2.1.2)</span>
      - <span id="section-appendix.b-2.2.1.3">Strike a spurious sentence
        about criticality of feedback, which was meant for feedback in
        general, not failure reports. In fact, failure reports are not
        critical to establishing and maintaining accurate authentication
        deployments. Still attributable to Ticket
        \#55.[¶](#section-appendix.b-2.2.1.3)</span>
      - <span id="section-appendix.b-2.2.1.4">Remove the content of
        section "Verifying External Destinations" and refer to
        I-D.ietf-dmarc-aggregate-reporting.[¶](#section-appendix.b-2.2.1.4)</span>
      - <span id="section-appendix.b-2.2.1.5">Remove the content of
        section "Security Considerations" and refer to
        I-D.ietf-dmarc-dmarcbis.[¶](#section-appendix.b-2.2.1.5)</span>
      - <span id="section-appendix.b-2.2.1.6">Slightly tweak the wording
        of the example in Appendix A.1 so that it makes sense standing
        alone.[¶](#section-appendix.b-2.2.1.6)</span>
      - <span id="section-appendix.b-2.2.1.7">Remove the sentence
        containing "must include any URI(s)", as the issue arose
        <span><https://mailarchive.ietf.org/arch/msg/dmarc/mFk0qiTCy8tzghRvcxus01W_Blw></span>.[¶](#section-appendix.b-2.2.1.7)</span>
      - <span id="section-appendix.b-2.2.1.8">Add paragraph in Security
        Considerations, noting that note that Organizational Domains are
        only an approximation...[¶](#section-appendix.b-2.2.1.8)</span>
      - <span id="section-appendix.b-2.2.1.9">Add a Transport section,
        mentioning DMARC conformance and failure report mail loops
        (Ticket \#28).[¶](#section-appendix.b-2.2.1.9)</span>

</div>

</div>

<div id="acknowledgements">

<div id="section-appendix.c" class="section">

## [Acknowledgements](#name-acknowledgements)

DMARC and the draft version of this document submitted to the
Independent Submission Editor were the result of lengthy efforts by an
informal industry consortium: DMARC.org (see <http://dmarc.org>).
Participating companies included Agari, American Greetings, AOL, Bank of
America, Cloudmark, Comcast, Facebook, Fidelity Investments, Google,
JPMorgan Chase & Company, LinkedIn, Microsoft, Netease, PayPal,
ReturnPath, The Trusted Domain Project, and Yahoo\!. Although the
contributors and supporters are too numerous to mention, notable
individual contributions were made by J. Trent Adams, Michael Adkins,
Monica Chew, Dave Crocker, Tim Draegen, Steve Jones, Franck Martin,
Brett McDowell, and Paul Midgen. The contributors would also like to
recognize the invaluable input and guidance that was provided early on
by J.D. Falk.[¶](#section-appendix.c-1)

Additional contributions within the IETF context were made by Kurt
Anderson, Michael Jack Assels, Les Barstow, Anne Bennett, Jim Fenton, J.
Gomez, Mike Jones, Scott Kitterman, Eliot Lear, John Levine, S.
Moonesamy, Rolf Sonneveld, Henry Timmes, and Stephen J.
Turnbull.[¶](#section-appendix.c-2)

</div>

</div>

<div id="authors-addresses">

<div id="section-appendix.d" class="section">

## [Authors' Addresses](#name-authors-addresses)

<div class="left" dir="auto">

<span class="fn nameRole">Steven M Jones
(<span class="role">editor</span>)</span>

</div>

<div class="left" dir="auto">

<span class="org">DMARC.org</span>

</div>

<div class="email">

<span>Email:</span> <smj@dmarc.org>

</div>

<div class="left" dir="auto">

<span class="fn nameRole">Alessandro Vesely
(<span class="role">editor</span>)</span>

</div>

<div class="left" dir="auto">

<span class="org">Tana</span>

</div>

<div class="email">

<span>Email:</span> <vesely@tana.it>

</div>

</div>

</div>
