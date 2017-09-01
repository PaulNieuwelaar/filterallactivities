# Filter 'All' Activities Dynamics 365

```javascript
function filterAllActivities() {
    $("#navActivities").click(function () {
        _filterAllActivitiesBase();
    });
}

function _filterAllActivitiesBase() {
    var frame = $("#areaActivitiesFrame");
    if (frame == null || frame.length == 0) {
        setTimeout(_filterAllActivitiesBase, 100);
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
