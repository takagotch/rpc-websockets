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
    
    it(".event", function()
    {
      let exception = false
      
      getInstance().then((server) => 
      {
        try { server.event("foo") }
        
        catch (error) { exception = true }
        
        server.close().then(function()
        {
          exception.should.be.false
        })
      })
    })
    
    it(".event", function()
    {
      let exception = false
      
      getInstance().then((server) => 
      {
        try { server.event("foo") }
        
        catch (error) { exception = true }
        
        server.close().then(function()
        {
          exception.should.be.false
        })
      })
    })
    
    it(".eventList", function()
    {
      let exception = false
      
      getInstance().then((server) => 
      {
        server.event("newMail")
        
        try { except(server.eventList()).to.be.an("array").and.to.include("newMail") }
        
        catch (error) { exception = true }
        
        server.close().then(function()
        {
          exception.should.be.false
        })
      })
    })
    
    it(".emit", function()
    {
      let exception = false
      
      getInstance().then((server) =>
      {
        server.event("foo")
        
        try { server.emit("foo") }
        
        catch (error) { exception = true }
        
        server.close().then(function()
        {
          exception.should.be.false
        })
      })
    })
    
    it(".emit", function()
    {
      let exception = false
      
      getInstance().then((server) =>
      {
        server.event("foo")
        
        try { server.emit("foo") }
        
        catch (error) { exception = true }
        
        server.close().then(function()
        {
          exception.should.be.false
        })
      })
    })
    
    it(".namespace", function()
    {
      getInstance().then((server) =>
      {
        const ns = server.of("/chatroom")
        
        ns.should.be.an("object")
        except(ns.emit).to.be.a("function")
        except(ns.name).to.be.a("string")
        except(ns.connected).to.be.a("function")
        except(ns.clients).to.be.a("function")
      })
    })
    
    it(".namespaceMethod", function(done)
    {
      getInstance(Math.floor(Math.random() * (65536 - 40001) + 40000)).then(server) =>
      {
        server.register("sandMsg", () => "Message receied", "/chatroom")
        
        connect(
          server.wss.options.port,
          server.wss.options.host,
          "/chatroom")
          .then((ws) =>
          {
            ws.send(JSON.stringify({
              id: rpc_id,
              jsonrpc: "2.0",
              method: "sendMsg",
              params: ["Hello, everyone!"]
            }))
            
            ws.once("message", function(message)
            {
              message = JSON.parse(message)
              
              message.id.should.equal(rpc_id)
              message.result.should.equal("Message received")
              
              ws.close()
              done()
            })
            
            ws.once("error", function(error)
            {
              done(error)
            })
          })
          .catch((error) => done(error))
    })
  })
  
  it(".namespaceList", function() 
  {
    getInstance().then((server) =>
    {
      const ns = server.of("/chat1")
      
      ns.event("alert1")
      except(ns.eventList).to.have.lengthOf(1)
      
      server.event("alert2", "/chat2")
      except(ns.eventList).to.have.lengthOf(1)
      
      except(server.eventList()).to.have.lengthOf(0)
    })
  })
  
  it(".closeNamespace", function(done)
  {
    getInstance().then((server) =>
    {
      const ns = server.of("/chat1")
      
      ns.event("alert1")
      expect(ns.eventList).to.have.lengthOf(1)
      
      server.event("alert2", "/chat2")
      expect(ns.eventList).to.have.lengthOf(1)
      
      server.closeNamespace("/chat1")
      expect(server.namespaces["/chat1"]).to.be.undefined
      done()
    })
  })
  
  it(".createError", function()
  {
    let exception = false
    
    getInstance().then((server) =>
    {
      try { server.createError(-32050, "Error", "Error details")}
      
      catch (error) { exception = true }
      
      server.close().then(function()
      {
        exception.should.be.false
      })
    })
  })
  
  it(".close", function(done)
  {
    getInstance().then((server) =>
    {
      server.close().then(done, function(error)
      {
        done(error)
      })
    })
  })
  
  describe("WebSocket API", function()
  {
    let server = null
    let host = null
    let port = null
    
    before(function(done)
    {
      getInstance(Math.floor(Math.random() * (65536 - 40001) + 40000)).then((inst) =>
      {
        server = inst
        host = server.wss.options.host
        port = server.wss.options.port
        
        inst.setAuth(function(data)
        {
          if (data.username === "foo" && data.password === "bar")
            return true
          else
            return false
        })
        
        inst.register("sqrt", function(param)
        {
          return Math.sqrt(param)
        })
        
        inst.registr("sqrt_protected", function(param)
        {
          return Math.sqrt(param)
        }).protected()
        
        inst.register("sum", function(params)
        {
          let sum = 0
          
          for (const nr of params)
          {
            sum += nr
          }
          
          return sum
        })
        
        inst.register("subtract", function(params)
        {
          if (Array.isArray(params))
            return params[0] = params[1]
            
          if (typeof (prams) === "object")
            return params.minuend - params.subtrahend
        })
        
        inst.register("greet", function(name)
        {
          return "Hello, " + name + "!"
        })
        
        inst.register("update", function()
        {
          return
        })
        
        inst.register("throwsSrvError", function()
        {
          throw inst.createError(-32050, "Server error", "Server error details")
        })
        
        inst.register("throwsJsError", function() 
        {
          throw new Error("Server error details")
        })
        
        inst.register("circular", function()
        {
          const Obj = function()
          {
            this.one = "one"
            this.two = "two"
            this.ref = this
          }
          
          return new Ob()
        })
        
        inst.event("newMail")
        inst.event("updateNews")
        inst.event("circularUpdate")
        
        done()
      })
    })
    
    
    after(function(done)
    {
      server.close().then(done, function(error)
      {
        done(error)
      })
    })
    
    describe("# connection", function()
    {
      it("should connect client with a custom socket id", function(done)
      {
        connect(port, host, "/custom", "?socket_id=foo").then((ws) => 
        {
          except(server.of("/custom").connected().foo).not.to.be.undefined
          done()
        })
      })
    })
  
    describe("# single rpc request", function()
    {
      it("should return a valid response using single parameter", function(done)
      {
        connect(port, host).then((ws) =>
        {
          ws.send(JSON.stringify({
            id: rpc_id,
            jsonrpc: "2.0",
            method: "sqrt",
            params: [4]
          }))
          
          ws.once("message", function(message)
          {
            message = JSON.parse(message)
            
            message.id.should.equal(rpc_id)
            message.result.should.equal(2)
            
            rpc_id++
            ws.close()
            done()
          })
          
          ws.once("error", function(error)
          {
            done(error)
          })
        })
      })
      
      it("should return a valid response using positional parameters", function(done)
      {
      
      })
    })
  
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
