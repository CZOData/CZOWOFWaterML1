CZOWOFWaterML1
==============

Everything about the CZO use of CUAHSI HIS WaterOneFlow and WaterML 1.x

This repository will cover anything involving the configuration and use of these services by the CZO community, from [the centralized services at CZO Central](http://central.criticalzone.org/pub_services.aspx) to more custom deployments by individual CZO's, such as the [Christina River CZO system](http://swrcsensors.dreamhosters.com/). That scope may include assessing and documenting how the [CZO shared vocabularies](http://sv.criticalzone.org/) are being used in these WOF services (for reference and comparison, here's the [CUAHSI HIS "Master Controlled Vocabulary Registry for ODM 1.1"](http://his.cuahsi.org/mastercvreg/cv11.aspx)). For reference, it's worth pointing out here that each CZO WOF endpoint on CZOC Central has a nice "home page" that presents all the web services available, including those based on WaterML 1.0, 1.1 and 2.0, as well as OGC WFS (I *think* this is HydroServer, but I'm not sure); as an example, [here's the service home page for Luquillo](http://water.sdsc.edu/czo_luquillo/Default.aspx).

### SiteTypeCV
* It's been pointed out that SiteTypeCV was introduced in ODM 1.1 (and corresponding WOF services). As a result, WOF endpoints that are based on service version 1.0 or are pointing to ODM 1.0 databases will not include a SiteType in the response. This may be the reason why the CZO shared vocabularies don't have a site type yet, though a [SiteTypeCV is available on the CUAHSI HIS ODM 1.1 CV's.](http://his.cuahsi.org/mastercvreg/edit_cv11.aspx?tbl=SiteTypeCV&id=853578079)
* I'm not seeing SiteType entries in the new CZO WOF 1.1 GetSiteInfo responses, at least for the Christina River end point. [See this example (a REST request).](http://water.sdsc.edu/czo_udel/REST/waterml_1_1.svc/siteinfo?location=czo_udel:STATION4)
* See [discussions on this topic in issue #1](https://github.com/CZOData/CZOWOFWaterML1/issues/1)

### Variables, VariableName CV, and occurrence of the same variable more than once on a site
* So far VariableName seems to be mostly in good shape (ie, for the one CZO for which I've assessed the GetVariables response, I only found one case of sloppiness -- two otherwise identical variable names except for the case used)
* Some VariableNames have an associated sampled medium, but many do not. eg, a Temperature w/o a SampleMedium or SiteType is potentially ambiguous.
* In some sites in the CZO Central WOF services -- but also in other WOF services -- the same variable name (ie, VariableNameCV) occurs more than once. I don't see any systematic information that can help me interpret each of those occurrences in a GetSiteInfo response. For example, are they two air temperature sensors at two different elevations along a tower? Or are they at the same depth, but simply different sensor deployments (eg, possibly different sensor models used at different times)? In order to map this information into vizer via an automatic metadata harvester, I need to be able to sort this out and code for it based on information in the response.
* See [discussions stemming from this topic in issue #2](https://github.com/CZOData/CZOWOFWaterML1/issues/2)

### "notes" and "site_property" content
* Currently the CZO WOF 1.0 GetSiteInfo response (at least for the Southern Sierra) has a "notes" element with state and county content; but those elements (or attributes -- can't remember) are empty. It would be very helpful to populate them as part of the process of standing up these WOF services and adding new sites.
* In the new CZO WOF 1.1 GetSiteInfo response (at least for Christina River), the "site_property" element replaces "notes". But the state and county elements are still empty.

### ulmo parsing issues with some elements in GetSiteInfo?
get_site_info response for some data series attributes (_method, _quality_control_level, _source, value_count, and variable_time_interval) are returned prepended with the WaterML namespace url; it should be stripped, as done with all other attributes. Will have to investigate if that's a problem with ulmo parsing or with the CUAHSI response encoding.
