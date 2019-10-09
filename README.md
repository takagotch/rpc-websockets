### rpc-websockets
---
https://github.com/elpheria/rpc-websockets

```js
// test/server.spec.js
"use strict";

const should = require("chai").should()
const expect = require("chai").expect
const WebSocket = require("ws")

const WebSocketServer = require("../dist").Server
const SERVER_HOST = "localhost"
const SERVER_PORT = 0 
let rpc_id = 1

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
  
  it(".register.protected", function()
  {
    let exception = false
    
    getInstance().then((server) => 
    {
      try
      {
        server.register("foo", function() {}).protected()
      }
      
      catch (error) { exception = true }
      
      server.close().then(function()
      {
        exceptoin.should.be.false
      })
    })
  })
  
  it(".register.public", function() 
  {
    let exception = false
    
    getInstance().then((server) =>
    {
      try
      {
        server.register("foo", function() {}).public()
      }
      
      catch (error) { exception = true }
      
      server.close().then(function()
      {
        exception.should.be.false
      })
    })
  })
  
  it(".setAuth", function()
  {
    let exception = false
    
    getInstance().then((server) => 
    {
      let exception = false
      
      getInstance().then((server) => 
      {
        try
        {
          server.register("foo", function() {}).public()
        }
        
        catch (error) { exception = true }
        
        server.close().then(function()
        {
          exception.should.be.false
        })
      })
    })
    
    it(".setAuth", function()
    {
      let exception = false
      
      getInstance().then((server) =>
      {
        try
        {
          server.setAuth(function() {})
        }
        
        catch (error) { exception = true }
        
        server.close().then(function()
        {
          exception.should.be.false
        })
      })
    })
    
    it(".")
  })
  
})













function getInstance(port, host)
{
  return new Promise((resolve, reject) => 
  {
    const wss = new WebSocketServer({
      host: host || SERVER_HOST,
      port: port || SERVER_PORT
    })
    
    wss.on("listening", () => resolve(wss))
  })
}

function connect(port, host, path, query)
{
  return new Promise((resolve, reject) => {
  {
    const client = new WebSocket("ws://" + (host || SERVER_HOST) +
      ":" + (port || SERVER_PORT) + (path || "/") + (query || ""))
      
    client.on("open", () => resolve(client))
    client.on("error", (error) => reject(error))
  })
}

function discount(client)
{
  return new Promise(function(resolve, reject)
  {
    client.close()
    resolve()
  })
}
```

```
```

```
```
