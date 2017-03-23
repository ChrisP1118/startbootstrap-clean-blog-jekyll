---
layout:     post
title:      "Excluding Azure Traffic Manager health checks (or any URL) from Application Insights telemetry"
subtitle:   "Implementing a custom ITelemetryProcessor to filter out certain URLs"
date:       2017-03-22 12:00:00
author:     "Chris"
header-img: "img/post-bg-01.jpg"
---

Azure's Traffic Manager service provides DNS-level load balancing. It performs a regular health check across all the possible endpoints, failing over if one becomes unresponsive.

I have a site that uses Azure Traffic Manager to balance traffic among some Azure Web Apps. I'm also using Application Insights to gather application telemetry. I want Application Insights to ignore those health checks from my Application Insights data -- they're just adding noise and using up my daily data.

To do this, I have a unique endpoint that's used only by Traffic Manager, which makes it easy to filter out. Then I wrote an ITelemetryProcessor that filters out requests.

The code:
```C#
namespace MagneTag.ApplicationInsights {

	public class ExcludeBotsTelemetryProcessor : ITelemetryProcessor
	{
		private ITelemetryProcessor _nextTelemetryProcessor { get; set; }

		public string ExcludedUrls { get; set; }

		public ExcludeBotsTelemetryProcessor(ITelemetryProcessor nextTelemetryProcessor)
		{
			_nextTelemetryProcessor = nextTelemetryProcessor;
		}

		public void Process(ITelemetry item)
		{
			RequestTelemetry request = item as RequestTelemetry;
			if (request != null)
			{
				foreach (string excludedUrl in ExcludedUrls.Split('|').Select(eu => eu.ToLower()))
					if (request.Url.AbsolutePath.ToLower() == excludedUrl)
						return;
			}

			_nextTelemetryProcessor.Process(item);
		}
	}
}
```

And then I added this to the ```TelemetryProcessors``` section of ```ApplicationInsights.config```:
```xml
<Add Type="MagneTag.ApplicationInsights.ExcludeBotsTelemetryProcessor, MagneTag.ApplicationInsights">
  <ExcludedUrls>/Home/Status</ExcludedUrls>
</Add>
```
