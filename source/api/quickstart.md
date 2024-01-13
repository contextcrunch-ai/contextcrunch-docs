# Quickstart

This is how to get started with the ContextCrunch API:

````{tab-set-code}

```{code-block} cURL
curl -X POST https://contextcrunch.com/api/call \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer YOUR_API_KEY" \
     -d '{
           "input": {
             "context": "This is some context",
             "prompt": "This is a question about the context",
             "type": "conversation",
             "compression_ratio": 0.95
           }
         }'
```


```{code-block} javascript
const axios = require('axios');

axios.post('https://contextcrunch.com/api/call', {
    input: {
        context: "This is some context",
        prompt: "This is a question about the context",
        type: "conversation",
        compression_ratio: 0.95
    }
}, {
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer YOUR_API_KEY'
    }
})
.then(response => console.log(response.data))
.catch(error => console.error(error));
```

```{code-block} python
# You should really check out our python integration instead!

import requests

response = requests.post(
    'https://contextcrunch.com/api/call',
    json={
        'input': {
            'context': 'This is some context',
            'prompt': 'This is a question about the context',
            'type': 'conversation',
            'compression_ratio': 0.95
        }
    },
    headers={'Authorization': 'Bearer YOUR_API_KEY'}
)
print(response.json())
```

```{code-block} ruby
require 'net/http'
require 'json'

uri = URI('https://contextcrunch.com/api/call')
request = Net::HTTP::Post.new(uri, 'Content-Type' => 'application/json', 'Authorization' => 'Bearer YOUR_API_KEY')
request.body = JSON.dump({
  input: {
    context: "This is some context",
    prompt: "This is a question about the context",
    type: "conversation",
    compression_ratio: 0.95
  }
})

response = Net::HTTP.start(uri.hostname, uri.port, use_ssl: uri.scheme == 'https') do |http|
  http.request(request)
end

puts response.body
```

````
