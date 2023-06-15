# Trigger

Custom JavaScript event system

## Quick example

Component:
```js
//top level
Trigger.on("tick", () => console.log("Tick"))
```

Will output "Tick" to console for each `Trigger("tick")` while component is alive (trigger is created onMount and removerd onDestroy)

## Quick reference

## Classes

<dl>
<dt><a href="#TriggerHandler">TriggerHandler</a></dt>
<dd><p>handler for an event, associated with a trigger</p>
</dd>
</dl>

## Constants

<dl>
<dt><a href="#Trigger">Trigger</a> : <code>function</code></dt>
<dd><p>Event handling system</p>
<p>Can be used as shorthand for Trigger.execute(trigger, ...args)
executes all non-transformative handlers associated with trigger (like array.forEach)</p>
</dd>
</dl>

## Functions

<dl>
<dt><a href="#execute">execute(trigger, ...args)</a></dt>
<dd><p>executes all non-transformative handlers associated with trigger
(like array.forEach)</p>
</dd>
<dt><a href="#poll">poll(trigger, ...args)</a> ⇒ <code>any</code></dt>
<dd><p>collects return values of all non-transformative handlers associated with trigger
(like array.map)</p>
</dd>
<dt><a href="#modify">modify(input, trigger, ...args)</a> ⇒ <code>any</code></dt>
<dd><p>applies all transformative handlers associated with trigger
in a chain
(like array.reduce)</p>
</dd>
<dt><a href="#handles">handles(trigger, callback, ...args)</a> ⇒ <code><a href="#TriggerHandler">Promise.&lt;TriggerHandler&gt;</a></code></dt>
<dd><p>creates non-transformative handler that exists for component&#39;s lifetime</p>
</dd>
<dt><a href="#modifies">modifies(trigger, callback, ...args)</a> ⇒ <code><a href="#TriggerHandler">Promise.&lt;TriggerHandler&gt;</a></code></dt>
<dd><p>creates transformative handler that exists for component&#39;s lifetime</p>
</dd>
<dt><a href="#createHandler">createHandler(trigger, callback, ...args)</a> ⇒ <code><a href="#TriggerHandler">TriggerHandler</a></code></dt>
<dd><p>creates non-transformative handler</p>
</dd>
<dt><a href="#createModifier">createModifier(trigger, callback, ...args)</a> ⇒ <code><a href="#TriggerHandler">TriggerHandler</a></code></dt>
<dd><p>creates transformative handler</p>
</dd>
<dt><a href="#createTrigger">createTrigger()</a> ⇒ <code><a href="#TriggerFunction">TriggerFunction</a></code></dt>
<dd><p>creates function that triggers using itself as a key</p>
</dd>
<dt><a href="#createPoll">createPoll()</a> ⇒ <code><a href="#PollFunction">PollFunction</a></code></dt>
<dd><p>creates function that triggers using itself as a key</p>
</dd>
<dt><a href="#createModification">createModification()</a> ⇒ <code><a href="#ModifierFunction">ModifierFunction</a></code></dt>
<dd><p>creates function that triggers using itself as a key</p>
</dd>
<dt><a href="#clearTrigger">clearTrigger(trigger)</a></dt>
<dd><p>cancels all handlers for a trigger and removes it from lists</p>
</dd>
<dt><a href="#on">on(trigger, callback, ...args)</a> ⇒ <code><a href="#TriggerHandler">Promise.&lt;TriggerHandler&gt;</a></code></dt>
<dd><p>creates non-transformative handler that exists for component&#39;s lifetime</p>
<p>shorthand to Trigger.handles()</p>
</dd>
<dt><a href="#once">once(trigger, callback, ...args)</a> ⇒ <code><a href="#TriggerHandler">Promise.&lt;TriggerHandler&gt;</a></code></dt>
<dd><p>creates non-transformative handler that exists for component&#39;s lifetime
or until first execution</p>
<p>shorthand to Trigger.handles().setOnce()</p>
</dd>
</dl>

## Typedefs

<dl>
<dt><a href="#HandlerCallback">HandlerCallback</a> ⇒ <code>any</code></dt>
<dd></dd>
<dt><a href="#TransformativeCallback">TransformativeCallback</a> ⇒ <code>any</code></dt>
<dd></dd>
<dt><a href="#TriggerFunction">TriggerFunction</a> : <code>function</code></dt>
<dd></dd>
<dt><a href="#PollFunction">PollFunction</a> ⇒ <code>any</code></dt>
<dd></dd>
<dt><a href="#ModifierFunction">ModifierFunction</a> ⇒ <code>any</code></dt>
<dd></dd>
</dl>

<a name="TriggerHandler"></a>

## TriggerHandler
handler for an event, associated with a trigger

**Kind**: global class  

* [TriggerHandler](#TriggerHandler)
    * [.cancel()](#TriggerHandler+cancel) ⇒ [<code>TriggerHandler</code>](#TriggerHandler)
    * [.setPriority(value)](#TriggerHandler+setPriority) ⇒ [<code>TriggerHandler</code>](#TriggerHandler)
    * [.setOnce(value)](#TriggerHandler+setOnce) ⇒ [<code>TriggerHandler</code>](#TriggerHandler)

<a name="TriggerHandler+cancel"></a>

### triggerHandler.cancel() ⇒ [<code>TriggerHandler</code>](#TriggerHandler)
cancels a handler so it never executes anymore and queues it for removal

**Kind**: instance method of [<code>TriggerHandler</code>](#TriggerHandler)  
**Returns**: [<code>TriggerHandler</code>](#TriggerHandler) - itself  
<a name="TriggerHandler+setPriority"></a>

### triggerHandler.setPriority(value) ⇒ [<code>TriggerHandler</code>](#TriggerHandler)
sets priority (higher = executed later)

**Kind**: instance method of [<code>TriggerHandler</code>](#TriggerHandler)  
**Returns**: [<code>TriggerHandler</code>](#TriggerHandler) - itself  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| value | <code>number</code> | <code>0</code> | new value (default is 0) |

<a name="TriggerHandler+setOnce"></a>

### triggerHandler.setOnce(value) ⇒ [<code>TriggerHandler</code>](#TriggerHandler)
sets flag for cancellation after next execution

**Kind**: instance method of [<code>TriggerHandler</code>](#TriggerHandler)  
**Returns**: [<code>TriggerHandler</code>](#TriggerHandler) - itself  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| value | <code>boolean</code> | <code>true</code> | new value |

<a name="Trigger"></a>

## Trigger : <code>function</code>
Event handling system

Can be used as shorthand for Trigger.execute(trigger, ...args)
executes all non-transformative handlers associated with trigger (like array.forEach)

**Kind**: global object 

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |
| ...args | <code>any</code> | arguments provided to each handler after its own arguments |

<a name="execute"></a>

## Trigger.execute(trigger, ...args)
executes all non-transformative handlers associated with trigger
(like array.forEach)

**Kind**: static method of [<code>Trigger</code>](#Trigger)  

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |
| ...args | <code>any</code> | arguments provided to each handler after its own arguments |

<a name="poll"></a>

## Trigger.poll(trigger, ...args) ⇒ <code>any</code>
collects return values of all non-transformative handlers associated with trigger
(like array.map)

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
**Returns**: <code>any</code> - - array of values returned by handlers  

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |
| ...args | <code>any</code> | arguments provided to each handler after its own arguments |

<a name="modify"></a>

## Trigger.modify(input, trigger, ...args) ⇒ <code>any</code>
applies all transformative handlers associated with trigger
in a chain
(like array.reduce)

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
**Returns**: <code>any</code> - - value returned by last handler  

| Param | Type | Description |
| --- | --- | --- |
| input | <code>any</code> | initial value |
| trigger | <code>any</code> | trigger key |
| ...args | <code>any</code> | arguments provided to each handler after its own arguments |

<a name="handles"></a>

## Trigger.handles(trigger, callback, ...args) ⇒ [<code>Promise.&lt;TriggerHandler&gt;</code>](#TriggerHandler)
creates non-transformative handler that exists for component's lifetime

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
**Returns**: [<code>Promise.&lt;TriggerHandler&gt;</code>](#TriggerHandler) - Promise that would resolve to handler
and can forward .setPriority, .setOnce and .cancel to it  

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |
| callback | [<code>HandlerCallback</code>](#HandlerCallback) | function |
| ...args | <code>any</code> | arguments passed to handler before trigger arguments |

<a name="modifies"></a>

## Trigger.modifies(trigger, callback, ...args) ⇒ [<code>Promise.&lt;TriggerHandler&gt;</code>](#TriggerHandler)
creates transformative handler that exists for component's lifetime

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
**Returns**: [<code>Promise.&lt;TriggerHandler&gt;</code>](#TriggerHandler) - Promise that would resolve to handler
and can forward .setPriority, .setOnce and .cancel to it  

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |
| callback | [<code>TransformativeCallback</code>](#TransformativeCallback) | function that transforms input |
| ...args | <code>any</code> | arguments passed to handler before trigger arguments |

<a name="createHandler"></a>

## Trigger.createHandler(trigger, callback, ...args) ⇒ [<code>TriggerHandler</code>](#TriggerHandler)
creates non-transformative handler

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
**Returns**: [<code>TriggerHandler</code>](#TriggerHandler) - handler  

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |
| callback | [<code>HandlerCallback</code>](#HandlerCallback) | function |
| ...args | <code>any</code> | arguments passed to handler before trigger arguments |

<a name="createModifier"></a>

## Trigger.createModifier(trigger, callback, ...args) ⇒ [<code>TriggerHandler</code>](#TriggerHandler)
creates transformative handler

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
**Returns**: [<code>TriggerHandler</code>](#TriggerHandler) - handler  

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |
| callback | [<code>TransformativeCallback</code>](#TransformativeCallback) | function that transforms input |
| ...args | <code>any</code> | arguments passed to handler before trigger arguments |

<a name="createTrigger"></a>

## Trigger.createTrigger() ⇒ [<code>TriggerFunction</code>](#TriggerFunction)
creates function that triggers using itself as a key

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
<a name="createPoll"></a>

## Trigger.createPoll() ⇒ [<code>PollFunction</code>](#PollFunction)
creates function that triggers using itself as a key

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
<a name="createModification"></a>

## Trigger.createModification() ⇒ [<code>ModifierFunction</code>](#ModifierFunction)
creates function that triggers using itself as a key

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
<a name="clearTrigger"></a>

## Trigger.clearTrigger(trigger)
cancels all handlers for a trigger and removes it from lists

**Kind**: static method of [<code>Trigger</code>](#Trigger)  

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |

<a name="on"></a>

## Trigger.on(trigger, callback, ...args) ⇒ [<code>Promise.&lt;TriggerHandler&gt;</code>](#TriggerHandler)
creates non-transformative handler that exists for component's lifetime

shorthand to Trigger.handles()

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
**Returns**: [<code>Promise.&lt;TriggerHandler&gt;</code>](#TriggerHandler) - Promise that would resolve to handler
and can forward .setPriority, .setOnce and .cancel to it  

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |
| callback | [<code>HandlerCallback</code>](#HandlerCallback) | function |
| ...args | <code>any</code> | arguments passed to handler before trigger arguments |

<a name="once"></a>

## Trigger.once(trigger, callback, ...args) ⇒ [<code>Promise.&lt;TriggerHandler&gt;</code>](#TriggerHandler)
creates non-transformative handler that exists for component's lifetime
or until first execution

shorthand to Trigger.handles().setOnce()

**Kind**: static method of [<code>Trigger</code>](#Trigger)  
**Returns**: [<code>Promise.&lt;TriggerHandler&gt;</code>](#TriggerHandler) - Promise that would resolve to handler
and can forward .setPriority, .setOnce and .cancel to it  

| Param | Type | Description |
| --- | --- | --- |
| trigger | <code>any</code> | trigger key |
| callback | [<code>HandlerCallback</code>](#HandlerCallback) | function |
| ...args | <code>any</code> | arguments passed to handler before trigger arguments |

<a name="HandlerCallback"></a>

## HandlerCallback ⇒ <code>any</code>
**Kind**: global typedef  
**Returns**: <code>any</code> - - return value for .poll (optional)  

| Param | Type | Description |
| --- | --- | --- |
| ...args | <code>any</code> | own arguments, passed before trigger's arguments |

<a name="TransformativeCallback"></a>

## TransformativeCallback ⇒ <code>any</code>
**Kind**: global typedef  
**Returns**: <code>any</code> - - modified value  

| Param | Type | Description |
| --- | --- | --- |
| input | <code>any</code> | initial value of return value of previous TransformativeHandler |
| ...args | <code>any</code> | own arguments, passed before trigger's arguments |

<a name="TriggerFunction"></a>

## TriggerFunction : <code>function</code>
**Kind**: global typedef  

| Param | Type | Description |
| --- | --- | --- |
| ...args | <code>any</code> | arguments, passed to handler after own arguments |

<a name="PollFunction"></a>

## PollFunction ⇒ <code>any</code>
**Kind**: global typedef  
**Returns**: <code>any</code> - - return values of handlers  

| Param | Type | Description |
| --- | --- | --- |
| ...args | <code>any</code> | arguments, passed to handler after own arguments |

<a name="ModifierFunction"></a>

## ModifierFunction ⇒ <code>any</code>
**Kind**: global typedef  
**Returns**: <code>any</code> - - initial value or return value of last handler  

| Param | Type | Description |
| --- | --- | --- |
| input | <code>any</code> | initial value |
| ...args | <code>any</code> | arguments, passed to handler after own arguments |



