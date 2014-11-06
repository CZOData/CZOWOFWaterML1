CZOWOFWaterML1
==============

Everything about the CZO use of CUAHSI HIS WaterOneFlow and WaterML 1.x

This repository will cover anything involving the configuration and use of these services by the CZO community, from [the centralized services at CZO Central](http://central.criticalzone.org/pub_services.aspx) to more custom deployments by individual CZO's, such as the [Christina River CZO system](http://swrcsensors.dreamhosters.com/). That scope may include assessing and documenting how the [CZO shared vocabularies](http://sv.criticalzone.org/) are being used in these WOF services (for reference and comparison, here's the [CUAHSI HIS "Master Controlled Vocabulary Registry for ODM 1.1"](http://his.cuahsi.org/mastercvreg/cv11.aspx)).

### SiteTypeCV
It's been pointed out that SiteTypeCV was introduced in ODM 1.1 (and corresponding WOF services). As a result, WOF endpoints that are based on service version 1.0 or are pointing to ODM 1.0 databases will not include a SiteType in the response. This may be the reason why the CZO shared vocabularies don't have a site type yet, though a [SiteTypeCV is available on the CUAHSI HIS ODM 1.1 CV's.](http://his.cuahsi.org/mastercvreg/edit_cv11.aspx?tbl=SiteTypeCV&id=853578079)
