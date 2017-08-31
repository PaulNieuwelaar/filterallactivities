# Filter 'All' Activities Dynamics 365

```javascript
FormHelper.FilterAllActivities = function () {
    $("#navActivities").click(function () {
        FormHelper._filterAllActivitiesBase();
    });
}

FormHelper._filterAllActivitiesBase = function () {
    var frame = $("#areaActivitiesFrame");
    if (frame == null || frame.length == 0) {
        setTimeout(FormHelper._filterAllActivitiesBase, 100);
        return;
    }

    frame.on("load", function () {
        var entityName = Xrm.Page.data.entity.getEntityName();
        var entity = entityName.charAt(0).toUpperCase() + entityName.substr(1);
        var doc = this.contentWindow.document;
        var filterOn = doc.getElementById("crmGrid_" + entity + "_ActivityPointers_datefilter");

        filterOn.value = "All";

        var evt = doc.createEvent("HTMLEvents");
        evt.initEvent("change", false, true);
        filterOn.dispatchEvent(evt);
    });
}
```
