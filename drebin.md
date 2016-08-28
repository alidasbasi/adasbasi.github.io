<div id="pieChart"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/3.4.4/d3.min.js"></script>
<script src="../d3pie.min.js"></script>
<script>
var pie = new d3pie("pieChart", {
	"header": {
		"title": {
			"text": "Drebin Veri Seti",
			"fontSize": 24,
			"font": "open sans"
		},
		"subtitle": {
			"text": "Drebin Veri Setine Ait Uygulamaların İzin İstatistikleri",
			"color": "#999999",
			"fontSize": 12,
			"font": "open sans"
		},
		"titleSubtitlePadding": 9
	},
	"footer": {
		"text": "[] ",
		"color": "#999999",
		"fontSize": 10,
		"font": "open sans",
		"location": "bottom-left"
	},
	"size": {
		"canvasWidth": 590,
		"pieOuterRadius": "90%"
	},
	"data": {
		"sortOrder": "value-desc",
		"content": [
			{
				"label": "INTERNET",
				"value": 5331,
				"color": "#2383c1"
			},
			{
				"label": "READ_PHONE_STATE",
				"value": 4937,
				"color": "#64a61f"
			},
			{
				"label": "WRITE_EXTERNAL_STORAGE",
				"value": 3719,
				"color": "#7b6788"
			},
			{
				"label": "ACCESS_NETWORK_STATE",
				"value": 3671,
				"color": "#a05c56"
			},
			{
				"label": "SEND_SMS",
				"value": 2996,
				"color": "#961919"
			},
			{
				"label": "RECEIVE_BOOT_COMPLETED",
				"value": 2669,
				"color": "#d8d239"
			},
			{
				"label": "ACCESS_WIFI_STATE",
				"value": 2427,
				"color": "#e98125"
			},
			{
				"label": "RECEIVE_SMS",
				"value": 2136,
				"color": "#d0743c"
			},
			{
				"label": "WAKE_LOCK",
				"value": 2129,
				"color": "#635122"
			},
			{
				"label": "READ_SMS",
				"value": 2079,
				"color": "#6ada6a"
			}
		]
	},
	"labels": {
		"outer": {
			"pieDistance": 32
		},
		"inner": {
			"hideWhenLessThanPercentage": 3
		},
		"mainLabel": {
			"fontSize": 11
		},
		"percentage": {
			"color": "#ffffff",
			"decimalPlaces": 0
		},
		"value": {
			"color": "#adadad",
			"fontSize": 11
		},
		"lines": {
			"enabled": true
		},
		"truncation": {
			"enabled": true
		}
	},
	"effects": {
		"pullOutSegmentOnClick": {
			"effect": "linear",
			"speed": 400,
			"size": 8
		}
	},
	"misc": {
		"gradient": {
			"enabled": true,
			"percentage": 100
		}
	}
});
</script>