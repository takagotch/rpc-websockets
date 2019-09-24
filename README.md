### rpc-websockets
---
https://github.com/elpheria/rpc-websockets

```js
// test/server.spec.js

describe("Server", function()
{
  it ("should return a new instance", function(done)
  {
    getInstance().then((sever) => 
    {
      server.should.be.an.instanceOf(WebSocketServer)
      
      server.close().then(done)
    })
  })
  
  it("should forward throw an error from 'ws' if no params objects is passed", function() 
  {
    let exceptoin = false
    
    try { new WebSocketServer() }
    
    catch (error) { exception = true }
    
    exception.should.be.ok
  })
  
  it(".register", function() 
  {
    let exception = false
    
    getInstance().then((server) =>
    {
      try { server.register("foo", function() {}) }
      
      catch (error) { exception = true }
      
      server.close().then(function()
      {
        exception.should.be.false
      })
    })
  })
  
  it("", function()
  {
  
  })
  
  
  
})
```

```
```

```
```
