# alexa-progressive-demo
demo of using progressive response using alexa skill kit. 
Changes can be seen in the lambda.py file 

custom skill builder is used to add the api clinet to skill. in this example default API client provided by alexa is used. 
SpeakDrivective is used to convert message to speech.

```
from ask_sdk_core.skill_builder import CustomSkillBuilder
from ask_sdk_core.api_client import DefaultApiClient
from ask_sdk_model.services.directive import (
    SendDirectiveRequest, Header, SpeakDirective)
sb = CustomSkillBuilder(api_client=DefaultApiClient())
```

The below function can be modified to send custom messages as additional parameter 

```
def get_progressive_response(handler_input):
    # type: (HandlerInput) -> None
    request_id_holder = handler_input.request_envelope.request.request_id
    directive_header = Header(request_id=request_id_holder)
    speech = SpeakDirective(speech="demo for progressive response")
    directive_request = SendDirectiveRequest(
        header=directive_header, directive=speech)

    directive_service_client = handler_input.service_client_factory.get_directive_service()
    directive_service_client.enqueue(directive_request)
    # time.sleep(5)
    return
```
