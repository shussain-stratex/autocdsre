# Establishing Service Level Objectives
This guide aims to provide a starting point for defining practical **Service Level Objectives**. For more information on
**Service Level Objectives** please reference
[Getting Started with Service Level Objectives]
All of the following quoted text is taken from [Site Reliability Engineering, Chapter 4 - Service Level Objectives](https://landing.google.com/sre/book/chapters/service-level-objectives.html)
unless otherwise specified.

### Objectives in Practice
> Start by thinking about (or finding out!) what your users care about, not what you can measure. Often, what your users
care about is difficult or impossible to measure, so you’ll end up approximating users’ needs in some way. However, if
you simply start with what’s easy to measure, you’ll end up with less useful SLOs. As a result, we’ve sometimes found
that working from desired objectives backward to specific indicators works better than choosing indicators and then
coming up with targets.

What I like to say is, "Think about how your users consume your service and the point at which your users would complain,
then determine if you have the metrics to support or deny their claim."

It is helpful to define what the optimal user experience is first, then see if you have the right metrics. Getting the
right metrics may require additional engineering, or switching a toolset, but this is better than reviewing your current
metrics en masse, and deciding from that pool what the value might be to an **SLO**.

##### Defining Objectives
> For maximum clarity, SLOs should specify how they’re measured and the conditions under which they’re valid. For instance, we might say the following (the second line is the same as the first, but relies on the SLI defaults of the previous section to remove redundancy):
>
> * 99% (averaged over 1 minute) of Get RPC calls will complete in less than 100 ms (measured across all the backend servers).
> * 99% of Get RPC calls will complete in less than 100 ms.
>
> If the shape of the performance curves are important, then you can specify multiple SLO targets:
>
> * 90% of Get RPC calls will complete in less than 1 ms.
> * 99% of Get RPC calls will complete in less than 10 ms.
> * 99.9% of Get RPC calls will complete in less than 100 ms.

When defining objectives there are a few categories most will get bucketed into,
* Latency
* Errors
* Throughput
* Saturation

Objectives do require that there is proper measurement, as mentioned [here](https://medium.com/@jerub/service-level-objectives-in-practice-ed1200502d5)
by Stephen Thorne, Senior SRE at Google, in reference to latency,
> Remember to measure this from the right place. Typically latency is always measured from a client that is a known
distance from the server. Ideally we measure every single request at the client and report back the statistics to a
monitoring system.
>
>  Two places that are bad to measure from are:
>
> * The server itself: because that server might have measurement glitches due to pauses in its own processing: such as
delay accepting the TCP connection, or delay writing data to the network.(why we're moving away from netdata and influxdb to datadog+splunk+sentry)
> * The client on the internet: because your latency numbers will vary wildly depending on their Internet connection.
You don’t want to wake someone up in the middle of the night because your app is suddenly popular in Australia!

##### Choosing Targets
> Choosing targets (SLOs) is not a purely technical activity because of the product and business implications, which
should be reflected in both the SLIs and SLOs (and maybe SLAs) that are selected. Similarly, it may be necessary to
trade off certain product attributes against others within the constraints posed by staffing, time to market, hardware
availability, and funding. While SRE should be part of this conversation, and advise on the risks and viability of
different options, we’ve learned a few lessons that can help make this a more productive discussion:
>
>  **Don’t pick a target based on current performance**
>  * While understanding the merits and limits of a system is essential, adopting values without reflection may lock
you into supporting a system that requires heroic efforts to meet its targets, and that cannot be improved without
significant redesign.
>
>  **Keep it simple**
>  * Complicated aggregations in SLIs can obscure changes to system performance, and are also harder to reason about.
>
>  **Avoid absolutes**
>  * While it’s tempting to ask for a system that can scale its load "infinitely" without any latency increase and that
is "always" available, this requirement is unrealistic. Even a system that approaches such ideals will probably take a
long time to design and build, and will be expensive to operate—and probably turn out to be unnecessarily better than
what users would be happy (or even delighted) to have.
>
>  **Have as few SLOs as possible**
>  * Choose just enough SLOs to provide good coverage of your system’s attributes. Defend the SLOs you pick: if you
can’t ever win a conversation about priorities by quoting a particular SLO, it’s probably not worth having that SLO.
However, not all product attributes are amenable to SLOs: it’s hard to specify "user delight" with an SLO.
>
>  **Perfection can wait**
>  * You can always refine SLO definitions and targets over time as you learn about a system’s behavior. It’s better to
start with a loose target that you tighten than to choose an overly strict target that has to be relaxed when you
discover it’s unattainable.
>
>  SLOs can—and should—be a major driver in prioritizing work for SREs and product developers, because they reflect what
users care about. A good SLO is a helpful, legitimate forcing function for a development team. But a poorly thought-out
SLO can result in wasted work if a team uses heroic efforts to meet an overly aggressive SLO, or a bad product if the
SLO is too lax. SLOs are a massive lever: use them wisely.

##### Recommended Reading
* [Site Reliability Engineering, Chapter 4 - Service Level Objectives](https://landing.google.com/sre/book/chapters/service-level-objectives.html)
* [Service Level Objectives in Practice](https://medium.com/@jerub/service-level-objectives-in-practice-ed1200502d5)
