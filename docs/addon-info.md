# Additional Verification Process Information

Some strategies allow the user to verify using different methods from different countries. 
In this case, it may be useful to know what country and method was used.

Let's look at an example ended conversation:

```json
{
    "id":"c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "userKey":"7dfb9ded-c38f-49ae-95e2-307283a0b1f6",
    "url":"https://sandbox.authologic.com/c/c12c1adc-3ff0-4d32-b95c-c593135c903e",
    "status":"FINISHED",
    "result":{
        "identity":{
            "status":"FINISHED",
            "errors": [],
            "user":{
                "person":{
                    "name":{
                      "firstName":"Jan",
                      "lastName":"Testowy"
                    }
                }
            }
        }
    },
    "info": [
        {
            "country": "PL",
            "method": "PSD2"
        }
    ]
}
```

In the example, the `info` section is visible. This is a table describing the verification process. 
Each element of this array represents information about the selected data source. The following data may appear here:

- `country`: the selected country used in the form of a two-letter ISO 3166-1 code
- `method`: the method that provided the data. This field may contain one of the following values:
  - `PSD2` - data source: Open Banking,
  - `TRANSFER_PL` - data source: Verification transfer,
  - `SCAN_SELFIE` - data source: Document scan and identity verification via selfie,
  - `MOBYWATEL` - data source: https://www.gov.pl/web/mobywatel,
  - `MOJEID_PL` - data source: https://www.mojeid.pl,
  - `EDO_APP` - data source: https://www.edoapp.pl,
  - `VERIMI_OPEN_BANKING` - data source: https://docs.verimi.de/#/openbanking,
  - `IDNOW_EID` - data source: https://www.idnow.io/products/idnow-eid,
  - `AUSWEIS_APP` - data source: https://www.ausweisapp.bund.de/en/home,
  - `MOJEID_CZ` - data source: https://www.mojeid.cz,
  - `BANKID_CZ` - data source: https://www.bankid.cz,
  - `BANKID_NO` - data source: https://bankid.no,
  - `BANKID_GB` - data source: https://oneid.uk,
  - `BANKID_SE` - data source: https://www.bankid.com,
  - `EPARAKSTS` - data source: https://www.eparaksts.lv,
  - `FREJA` - data source: https://frejaeid.com,
  - `ITSME` - data source: https://www.itsme-id.com,
  - `MITID` - data source: https://www.mitid.dk,
  - `IDIN` - data source: https://www.idin.nl,
  - `FINNISH_TRUST_NETWORK` - data source: https://www.kyberturvallisuuskeskus.fi/en/our-activities/regulation-and-supervision/electronic-identification#9970-2 https://www.nets.eu/developer/e-ident/eids/Pages/BankIDFI.aspx,
  - `LIDENTITE_NUMERIQUE_LAPOSTE` - data source: https://lidentitenumerique.laposte.fr,
  - `FRANCE_CONNECT` - data source: https://franceconnect.gouv.fr,
  - `DOCAPOSTE_ID360_FR` - data source: https://www.docaposte.com/en/solutions/id360,
  - `E_ID_CARD_BE` - data source: https://eid.belgium.be,
  - `E_ID_CARD_EE` - data source: https://www.id.ee/en/id-card/,
  - `E_ID_CARD_PT` - data source: https://www.autenticacao.gov.pt/o-cartao-de-cidadao,
  - `E_ID_CARD_FI` - data source: https://dvv.fi/,
  - `E_ID_CARD_LV` - data source: https://www.pmlp.gov.lv/en/electronic-personal-certificate-and-identity
  - `E_ID_CARD_LT` - data source: https://www.nsc.vrm.lt/default_en.htm,
  - `E_ID_CARD_RS` - http://ca.mup.gov.rs/ca/ca_en/start/kes/,
  - `UAEPASS` - data source: https://uaepass.ae,
  - `BRICK` - data source: https://www.onebrick.io,
  - `MOBILEID_EE`, `MOBILEID_LT` - data source: https://www.mobile-id.lt,
  - `SPID` - data source: https://www.mobile-id.lt,
  - `SMART_ID` - data source: https://www.smart-id.com,
  - `YOTI` - data source: https://www.yoti.com,
  - `GOV_DB_NIMC` - data source: https://nimc.gov.ng,
  - `GOV_DB_SERPRO` - data source: https://www.serpro.gov.br,
  - `AUTENTICACAO_GOV_PT` - data source: https://www.autenticacao.gov.pt

<!-- theme: info -->
> #### TIP
>
> Please note that the content of the `method` field may change over time as new data sources become available.

<!-- theme: warning -->
> #### WARNING
>
> Both `country`, `method` and the entire `info` section do not have to appear - it all depends on the strategy 
> used and the specificity of the selected data sources.

<!-- theme: info -->
>
> Despite our sincere intentions, it is difficult to create perfect technical documentation.
> If you have an idea on how to improve this documentation, or you have trouble understanding any section,
> please email us at tech-support@authologic.com
