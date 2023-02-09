---
description: A list of Available events in OneConfig.
---

# Available Events

Events are split into **types**, which can be specified by the parameter type set on your method you are `@Subscribe`-ing.

Each Event has a purpose, for example `ChatReceiveEvent`, which is fired every time the client receives a message. These are useful because if you want to do something when a message is received, like check its contents for a series of letters, you can do it easily!

{% hint style="danger" %}
Remember all `@Subscribe` event methods must not be static!
{% endhint %}

## List of Available Events

{% content-ref url="chatreceiveevent.md" %}
[chatreceiveevent.md](chatreceiveevent.md)
{% endcontent-ref %}

{% content-ref url="tickevent.md" %}
[tickevent.md](tickevent.md)
{% endcontent-ref %}

{% content-ref url="initializationevent.md" %}
[initializationevent.md](initializationevent.md)
{% endcontent-ref %}

{% content-ref url="hudrenderevent.md" %}
[hudrenderevent.md](hudrenderevent.md)
{% endcontent-ref %}

{% content-ref url="locrawevent.md" %}
[locrawevent.md](locrawevent.md)
{% endcontent-ref %}
