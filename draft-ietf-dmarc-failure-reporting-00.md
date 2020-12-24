Internet-Draft

DMARC Failure Reporting

December 2020

Jones & Vesely

Expires 27 June 2021

\[Page\]

<div id="external-metadata" class="document-information">

</div>

<div id="internal-metadata" class="document-information">

  - Workgroup:  
    DMARC Working Group

  - Internet-Draft:  
    draft-ietf-dmarc-failure-reporting-00

  - Obsoletes:  
    [7489](https://www.rfc-editor.org/rfc/rfc7489) (if approved)

  - Published:  
    24 December 2020

  - Intended Status:  
    Standards Track

  - Expires:  
    27 June 2021

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

This Internet-Draft will expire on 27 June
2021.[¶](#section-boilerplate.1-4)

</div>

</div>

<div id="copyright">

<div id="section-boilerplate.2" class="section">

## [Copyright Notice](#name-copyright-notice)

Copyright (c) 2020 IETF Trust and the persons identified as the document
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
    
      - 
        
        <div id="section-toc.1-1.5.2.1">
        
        [5.1](#section-5.1).  [Attacks on Reporting
        URIs](#name-attacks-on-reporting-uris)[¶](#section-toc.1-1.5.2.1.1)
        
        </div>
    
      - 
        
        <div id="section-toc.1-1.5.2.2">
        
        [5.2](#section-5.2).  [DNS
        Security](#name-dns-security)[¶](#section-toc.1-1.5.2.2.1)
        
        </div>
    
      - 
        
        <div id="section-toc.1-1.5.2.3">
        
        [5.3](#section-5.3).  [External Reporting
        Addresses](#name-external-reporting-addresse)[¶](#section-toc.1-1.5.2.3.1)
        
        </div>
    
      - 
        
        <div id="section-toc.1-1.5.2.4">
        
        [5.4](#section-5.4).  [Secure
        Protocols](#name-secure-protocols)[¶](#section-toc.1-1.5.2.4.1)
        
        </div>
    
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
    
    [](#section-appendix.b)[Acknowledgements](#name-acknowledgements)[¶](#section-toc.1-1.9.1)
    
    </div>

  - 
    
    <div id="section-toc.1-1.10">
    
    [](#section-appendix.c)[Authors'
    Addresses](#name-authors-addresses)[¶](#section-toc.1-1.10.1)
    
    </div>

</div>

</div>

<div id="introduction">

<div id="section-1" class="section">

## [1.](#section-1)[Introduction](#name-introduction)

Domain-based Message Authentication, Reporting, and Conformance (DMARC)
<span>\[[RFC7489](#RFC7489)\]</span> is a scalable mechanism by which a
mail-originating organization can express domain-level policies and
preferences for message validation, disposition, and reporting, that a
mail-receiving organization can use to improve mail handling. This
document focuses on one type of reporting that can be requested under
DMARC.[¶](#section-1-1)

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
<span>\[[RFC7489](#RFC7489)\]</span>, specifically the terminology and
definitions section.[¶](#section-2-3)

</div>

</div>

<div id="failure-reports">

<div id="section-3" class="section">

## [3.](#section-3)[Failure Reports](#name-failure-reports)

Providing Domain Owners with visibility into how Mail Receivers
implement and enforce the DMARC mechanism in the form of feedback is
critical to establishing and maintaining accurate authentication
deployments. Failure reports can supply more detailed information about
messages that failed to authenticate, enabling the Domain Owner to
determine exactly what might be causing those specific
failures.[¶](#section-3-1)

Failure reports are normally generated and sent almost immediately after
the Mail Receiver detects a DMARC failure. Rather than waiting for an
aggregate report, these reports are useful for quickly notifying the
Domain Owners when there is an authentication failure. Whether the
failure is due to an infrastructure problem or the message is
inauthentic, failure reports also provide more information about the
failed message than is available in an aggregate
report.[¶](#section-3-2)

These reports SHOULD include any URI(s) from the message that failed
authentication. These reports SHOULD include as much of the message and
message header as is reasonable to support the Domain Owner's
investigation into what caused the message to fail authentication and
track down the sender.[¶](#section-3-3)

When a Domain Owner requests failure reports for the purpose of forensic
analysis, and the Mail Receiver is willing to provide such reports, the
Mail Receiver generates and sends a message using the format described
in <span>\[[RFC6591](#RFC6591)\]</span>; this document updates that
reporting format, as described in [Section
3.1](#reporting-format-update).[¶](#section-3-4)

The destination(s) and nature of the reports are defined by the "ruf"
and "fo" tags as defined in (<span>\[[RFC7489](#RFC7489)\]</span>
general-record-format).[¶](#section-3-5)

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

It is possible to specify destinations for the different reports that
are outside the authority of the Domain Owner making the request. This
allows domains that do not operate mail servers to request reports and
have them go someplace that is able to receive and process
them.[¶](#section-3.2-1)

Without checks, this would allow a bad actor to publish a DMARC policy
record that requests that reports be sent to a victim address, and then
send a large volume of mail that will fail both DKIM and SPF checks to a
wide variety of destinations; the victim will in turn be flooded with
unwanted reports. Therefore, a verification mechanism is
included.[¶](#section-3.2-2)

When a Mail Receiver discovers a DMARC policy in the DNS, and the
Organizational Domain at which that record was discovered is not
identical to the Organizational Domain of the host part of the authority
component of a <span>\[[RFC3986](#RFC3986)\]</span> specified in the
"rua" or "ruf" tag, the following verification steps are to be
taken:[¶](#section-3.2-3)

1.  
    
    <div id="section-3.2-4.1">
    
    Extract the host portion of the authority component of the URI. Call
    this the "destination host", as it refers to a Report
    Receiver.[¶](#section-3.2-4.1.1)
    
    </div>

2.  
    
    <div id="section-3.2-4.2">
    
    Prepend the string "\_report.\_dmarc".[¶](#section-3.2-4.2.1)
    
    </div>

3.  
    
    <div id="section-3.2-4.3">
    
    Prepend the domain name from which the policy was retrieved, after
    conversion to an A-label if needed.[¶](#section-3.2-4.3.1)
    
    </div>

4.  
    
    <div id="section-3.2-4.4">
    
    Query the DNS for a TXT record at the constructed name. If the
    result of this request is a temporary DNS error of some kind (e.g.,
    a timeout), the Mail Receiver MAY elect to temporarily fail the
    delivery so the verification test can be repeated
    later.[¶](#section-3.2-4.4.1)
    
    </div>

5.  
    
    <div id="section-3.2-4.5">
    
    For each record returned, parse the result as a series of
    "tag=value" pairs, i.e., the same overall format as the policy
    record (see (<span>\[[RFC7489](#RFC7489)\]</span>
    formal-definition)). In particular, the "v=DMARC1;" tag is mandatory
    and MUST appear first in the list. Discard any that do not pass this
    test.[¶](#section-3.2-4.5.1)
    
    </div>

6.  
    
    <div id="section-3.2-4.6">
    
    If the result includes no TXT resource records that pass basic
    parsing, a positive determination of the external reporting
    relationship cannot be made; stop.[¶](#section-3.2-4.6.1)
    
    </div>

7.  
    
    <div id="section-3.2-4.7">
    
    If at least one TXT resource record remains in the set after
    parsing, then the external reporting arrangement was authorized by
    the Report Receiver.[¶](#section-3.2-4.7.1)
    
    </div>

8.  
    
    <div id="section-3.2-4.8">
    
    If a "rua" or "ruf" tag is thus discovered, replace the
    corresponding value extracted from the domain's DMARC policy record
    with the one found in this record. This permits the Report Receiver
    to override the report destination. However, to prevent loops or
    indirect abuse, the overriding URI MUST use the same destination
    host from the first step.[¶](#section-3.2-4.8.1)
    
    </div>

For example, if a DMARC policy query for "blue.example.com" contained
"rua=mailto:reports@red.example.net", the host extracted from the latter
("red.example.net") does not match "blue.example.com", so this procedure
is enacted. A TXT query for
"blue.example.com.\_report.\_dmarc.red.example.net" is issued. If a
single reply comes back containing a tag of "v=DMARC1;", then the
relationship between the two is confirmed. Moreover, "red.example.net"
has the opportunity to override the report destination requested by
"blue.example.com" if needed.[¶](#section-3.2-5)

Where the above algorithm fails to confirm that the external reporting
was authorized by the Report Receiver, the URI MUST be ignored by the
Mail Receiver generating the report. Further, if the confirming record
includes a URI whose host is again different than the domain publishing
that override, the Mail Receiver generating the report MUST NOT generate
a report to either the original or the override URI.[¶](#section-3.2-6)

A Report Receiver publishes such a record in its DNS if it wishes to
receive reports for other domains.[¶](#section-3.2-7)

A Report Receiver that is willing to receive reports for any domain can
use a wildcard DNS record. For example, a TXT resource record at
"\*.\_report.\_dmarc.example.com" containing at least "v=DMARC1;"
confirms that example.com is willing to receive DMARC reports for any
domain.[¶](#section-3.2-8)

If the Report Receiver is overcome by volume, it can simply remove the
confirming DNS record. However, due to positive caching, the change
could take as long as the time-to-live (TTL) on the record to go into
effect.[¶](#section-3.2-9)

A Mail Receiver might decide not to enact this procedure if, for
example, it relies on a local list of domains for which external
reporting addresses are
permitted.[¶](#section-3.2-10)

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

This section discusses security issues related to DMARC reporting, and
possible
remediations.[¶](#section-5-1)

<div id="attacks-on-reporting-uris">

<div id="section-5.1" class="section">

### [5.1.](#section-5.1)[Attacks on Reporting URIs](#name-attacks-on-reporting-uris)

URIs published in DNS TXT records are well-understood possible targets
for attack. Specifications such as <span>\[[RFC1035](#RFC1035)\]</span>
and <span>\[[RFC2142](#RFC2142)\]</span> either expose or cause the
exposure of email addresses that could be flooded by an attacker, for
example; MX, NS, and other records found in the DNS advertise potential
attack destinations; common DNS names such as "www" plainly identify the
locations at which particular services can be found, providing
destinations for targeted denial-of-service or penetration
attacks.[¶](#section-5.1-1)

Thus, Domain Owners will need to harden these addresses against various
attacks, including but not limited to:[¶](#section-5.1-2)

  - 
    
    <div id="section-5.1-3.1">
    
    high-volume denial-of-service attacks;[¶](#section-5.1-3.1.1)
    
    </div>

  - 
    
    <div id="section-5.1-3.2">
    
    deliberate construction of malformed reports intended to identify or
    exploit parsing or processing
    vulnerabilities;[¶](#section-5.1-3.2.1)
    
    </div>

  - 
    
    <div id="section-5.1-3.3">
    
    deliberate construction of reports containing false claims for the
    Submitter or Reported-Domain fields, including the possibility of
    false data from compromised but known Mail
    Receivers.[¶](#section-5.1-3.3.1)
    
    </div>

</div>

</div>

<div id="dns-security">

<div id="section-5.2" class="section">

### [5.2.](#section-5.2)[DNS Security](#name-dns-security)

The DMARC mechanism and its underlying technologies (SPF, DKIM) depend
on the security of the DNS. To reduce the risk of subversion of the
DMARC mechanism due to DNS-based exploits, serious consideration should
be given to the deployment of DNSSEC in parallel with the deployment of
DMARC by both Domain Owners and Mail Receivers.[¶](#section-5.2-1)

Publication of data using DNSSEC is relevant to Domain Owners and
third-party Report Receivers. DNSSEC-aware resolution is relevant to
Mail Receivers and Report
Receivers.[¶](#section-5.2-2)

</div>

</div>

<div id="external-report-addresses">

<div id="section-5.3" class="section">

### [5.3.](#section-5.3)[External Reporting Addresses](#name-external-reporting-addresse)

To avoid abuse by bad actors, reporting addresses generally have to be
inside the domains about which reports are requested. In order to
accommodate special cases such as a need to get reports about domains
that cannot actually receive mail, [Section
3.2](#verifying-external-destinations) describes a DNS-based mechanism
for verifying approved external reporting.[¶](#section-5.3-1)

The obvious consideration here is an increased DNS load against domains
that are claimed as external recipients. Negative caching will mitigate
this problem, but only to a limited extent, mostly dependent on the
default TTL in the domain's SOA record.[¶](#section-5.3-2)

Where possible, external reporting is best achieved by having the report
be directed to domains that can receive mail and simply having it
automatically forwarded to the desired external
destination.[¶](#section-5.3-3)

Note that the addresses shown in the "ruf" tag receive more information
that might be considered private data, since it is possible for actual
email content to appear in the failure reports. The URIs identified
there are thus more attractive targets for intrusion attempts than those
found in the "rua" tag. Moreover, attacking the DNS of the subject
domain to cause failure data to be routed fraudulently to an attacker's
systems may be an attractive prospect. Deployment of
<span>\[[RFC4033](#RFC4033)\]</span> is advisable if this is a
concern.[¶](#section-5.3-4)

The verification mechanism presented in [Section
3.2](#verifying-external-destinations) is currently not mandatory
("MUST") but strongly recommended ("SHOULD"). It is possible that it
would be elevated to a "MUST" by later security
review.[¶](#section-5.3-5)

</div>

</div>

<div id="secure-protocols">

<div id="section-5.4" class="section">

### [5.4.](#section-5.4)[Secure Protocols](#name-secure-protocols)

This document encourages use of secure transport mechanisms to prevent
loss of private data to third parties that may be able to monitor such
transmissions. Unencrypted mechanisms should be
avoided.[¶](#section-5.4-1)

In particular, a message that was originally encrypted or otherwise
secured might appear in a report that is not sent securely, which could
reveal private information.[¶](#section-5.4-2)

</div>

</div>

</div>

</div>

<div id="section-6" class="section">

## [6.](#section-6)[Normative References](#name-normative-references)

  - \[RFC1035\]  
    <span class="refAuthor">Mockapetris, P.</span>,
    <span class="refTitle">"Domain names - implementation and
    specification"</span>, <span class="seriesInfo">STD 13</span>,
    <span class="seriesInfo">RFC 1035</span>,
    <span class="seriesInfo">DOI 10.17487/RFC1035</span>, November 1987,
    <span>\<<https://www.rfc-editor.org/info/rfc1035>\></span>.
  - \[RFC2119\]  
    <span class="refAuthor">Bradner, S.</span>,
    <span class="refTitle">"Key words for use in RFCs to Indicate
    Requirement Levels"</span>, <span class="seriesInfo">BCP 14</span>,
    <span class="seriesInfo">RFC 2119</span>,
    <span class="seriesInfo">DOI 10.17487/RFC2119</span>, March 1997,
    <span>\<<https://www.rfc-editor.org/info/rfc2119>\></span>.
  - \[RFC3986\]  
    <span class="refAuthor">Berners-Lee,
    T.</span><span class="refAuthor">, Fielding,
    R.</span><span class="refAuthor">, and L. Masinter</span>,
    <span class="refTitle">"Uniform Resource Identifier (URI): Generic
    Syntax"</span>, <span class="seriesInfo">STD 66</span>,
    <span class="seriesInfo">RFC 3986</span>,
    <span class="seriesInfo">DOI 10.17487/RFC3986</span>, January 2005,
    <span>\<<https://www.rfc-editor.org/info/rfc3986>\></span>.
  - \[RFC6591\]  
    <span class="refAuthor">Fontana, H.</span>,
    <span class="refTitle">"Authentication Failure Reporting Using the
    Abuse Reporting Format"</span>, <span class="seriesInfo">RFC
    6591</span>, <span class="seriesInfo">DOI 10.17487/RFC6591</span>,
    April 2012,
    <span>\<<https://www.rfc-editor.org/info/rfc6591>\></span>.
  - \[RFC7489\]  
    <span class="refAuthor">Kucherawy, M.,
    Ed.</span><span class="refAuthor"> and E. Zwicky, Ed.</span>,
    <span class="refTitle">"Domain-based Message Authentication,
    Reporting, and Conformance (DMARC)"</span>,
    <span class="seriesInfo">RFC 7489</span>,
    <span class="seriesInfo">DOI 10.17487/RFC7489</span>, March 2015,
    <span>\<<https://www.rfc-editor.org/info/rfc7489>\></span>.

</div>

<div id="section-7" class="section">

## [7.](#section-7)[Informative References](#name-informative-references)

  - \[RFC2142\]  
    <span class="refAuthor">Crocker, D.</span>,
    <span class="refTitle">"Mailbox Names for Common Services, Roles and
    Functions"</span>, <span class="seriesInfo">RFC 2142</span>,
    <span class="seriesInfo">DOI 10.17487/RFC2142</span>, May 1997,
    <span>\<<https://www.rfc-editor.org/info/rfc2142>\></span>.
  - \[RFC4033\]  
    <span class="refAuthor">Arends, R.</span><span class="refAuthor">,
    Austein, R.</span><span class="refAuthor">, Larson,
    M.</span><span class="refAuthor">, Massey,
    D.</span><span class="refAuthor">, and S. Rose</span>,
    <span class="refTitle">"DNS Security Introduction and
    Requirements"</span>, <span class="seriesInfo">RFC 4033</span>,
    <span class="seriesInfo">DOI 10.17487/RFC4033</span>, March 2005,
    <span>\<<https://www.rfc-editor.org/info/rfc4033>\></span>.
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

The Domain Owner from the previous example has used the aggregate
reporting to discover some messaging systems that had not yet
implemented DKIM correctly, but they are still seeing periodic
authentication failures. In order to diagnose these intermittent
problems, they wish to request per-message failure reports when
authentication failures occur.[¶](#section-a.1-1)

Not all Receivers will honor such a request, but the Domain Owner feels
that any reports it does receive will be helpful enough to justify
publishing this record. The default per-message report format
(<span>\[[RFC6591](#RFC6591)\]</span>) meets the Domain Owner's needs in
this scenario.[¶](#section-a.1-2)

The Domain Owner accomplishes this by adding the following to its policy
record from (<span>\[[RFC7489](#RFC7489)\]</span>
domain-owner-example):[¶](#section-a.1-3)

  - <span id="section-a.1-4.1">Per-message failure reports should be
    sent via email to the address "auth-reports@example.com"
    ("ruf=mailto:auth-reports@example.com")[¶](#section-a.1-4.1)</span>

The DMARC policy record might look like this when retrieved using a
common command-line tool (the output shown would appear on a single line
but is wrapped here for publication):[¶](#section-a.1-5)

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

<div id="acknowledgements">

<div id="section-appendix.b" class="section">

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
by J.D. Falk.[¶](#section-appendix.b-1)

Additional contributions within the IETF context were made by Kurt
Anderson, Michael Jack Assels, Les Barstow, Anne Bennett, Jim Fenton, J.
Gomez, Mike Jones, Scott Kitterman, Eliot Lear, John Levine, S.
Moonesamy, Rolf Sonneveld, Henry Timmes, and Stephen J.
Turnbull.[¶](#section-appendix.b-2)

</div>

</div>

<div id="authors-addresses">

<div id="section-appendix.c" class="section">

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
