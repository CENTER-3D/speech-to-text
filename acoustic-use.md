---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Using a custom acoustic model
{: #acousticUse}

Once you create and train your custom acoustic model, you can use it in speech recognition requests. You use the `acoustic_customization_id` query parameter to specify the custom acoustic model for a request, as shown in the following examples. You must issue the request with service credentials for the instance of the service that owns the model.
{: shortdesc}

You can also specify a custom language model to be used with the request, which can increase transcription accuracy. For more information, see [Using custom language and custom acoustic models during speech recognition](/docs/services/speech-to-text/acoustic-both.html#useBothRecognize).

You can create multiple custom acoustic models for the same or different domains or environments. However, you can specify only one custom acoustic model at a time with the `acoustic_customization_id` parameter.

-   For the WebSocket interface, use the `/v1/recognize` method. The specified custom model is used for all requests that are sent over the connection.

    ```javascript
    var token = {authentication-token};
    var wsURI = 'wss://stream.watsonplatform.net/speech-to-text/api/v1/recognize'
      + '?watson-token=' + token
      + '&model=en-US_NarrowbandModel'
      + '&acoustic_customization_id={customization_id}';
    var websocket = new WebSocket(wsURI);
    ```
    {: codeblock}

   For more information, see [The WebSocket interface](/docs/services/speech-to-text/websockets.html).
-   For the HTTP interface, use the `POST /v1/recognize` method. The specified custom model is used for that request.

    ```bash
    curl -X POST -u "{username}:{password}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file1.flac
    "https://stream.watsonplatform.net/speech-to-text/api/v1/recognize?acoustic_customization_id={customization_id}"
    ```
    {: pre}

    For more information, see [The HTTP interface](/docs/services/speech-to-text/http.html).
-   For the asynchronous HTTP interface, use the `POST /v1/recognitions` method. The specified custom model is used for that request.

    ```bash
    curl -X POST -u "{username}:{password}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file.flac
    "https://stream.watsonplatform.net/speech-to-text/api/v1/recognitions?acoustic_customization_id={customization_id}"
    ```
    {: pre}

    For more information, see [The asynchronous HTTP interface](/docs/services/speech-to-text/async.html).

You can omit the language model from the request if the custom model is based on the default model, `en-US_BroadbandModel`. Otherwise, you must use the `model` parameter to specify the base model, as shown for the WebSocket example. A custom model can be used only with the base model for which it is created.
