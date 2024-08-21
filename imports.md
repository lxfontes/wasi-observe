<h1><a name="imports">World imports</a></h1>
<ul>
<li>Imports:
<ul>
<li>interface <a href="#wasi_observe_types"><code>wasi:observe/types</code></a></li>
<li>interface <a href="#wasi_observe_logging"><code>wasi:observe/logging</code></a></li>
<li>interface <a href="#wasi_observe_metrics"><code>wasi:observe/metrics</code></a></li>
<li>interface <a href="#wasi_observe_tracing"><code>wasi:observe/tracing</code></a></li>
</ul>
</li>
</ul>
<h2><a name="wasi_observe_types"></a>Import interface wasi:observe/types</h2>
<hr />
<h3>Types</h3>
<h4><a name="tag_value"></a><code>variant tag-value</code></h4>
<h5>Variant Cases</h5>
<ul>
<li>
<p><a name="tag_value.blank"></a><code>blank</code></p>
</li>
<li>
<p><a name="tag_value.error"></a><code>error</code>: <code>string</code></p>
<p>NOTE(lxf): This is where a 'shared wasi error interface' would be useful.
</li>
<li>
<p><a name="tag_value.value"></a><code>value</code>: <code>string</code></p>
</li>
</ul>
<h4><a name="tags"></a><code>type tags</code></h4>
<p><a href="#tags"><a href="#tags"><code>tags</code></a></a></p>
<p>
## <a name="wasi_observe_logging"></a>Import interface wasi:observe/logging
<p>Logging is a logging API intended to let users emit log messages with
simple priority levels, a message, and optional contextual attributes.</p>
<hr />
<h3>Types</h3>
<h4><a name="tags"></a><code>type tags</code></h4>
<p><a href="#tags"><a href="#tags"><code>tags</code></a></a></p>
<p>
#### <a name="level"></a>`enum level`
<p>A log level, describing a kind of message.</p>
<h5>Enum Cases</h5>
<ul>
<li>
<p><a name="level.debug"></a><code>debug</code></p>
<p>Describes messages likely to be of interest to someone debugging a
program.
</li>
<li>
<p><a name="level.info"></a><code>info</code></p>
<p>Describes messages likely to be of interest to someone monitoring a
program.
</li>
<li>
<p><a name="level.warn"></a><code>warn</code></p>
<p>Describes messages indicating hazardous situations.
</li>
<li>
<p><a name="level.error"></a><code>error</code></p>
<p>Describes messages indicating serious errors.
</li>
</ul>
<hr />
<h3>Functions</h3>
<h4><a name="set_tags"></a><code>set-tags: func</code></h4>
<p>Adds contextual attributes to the current log context.</p>
<p>Subsequent <a href="#log"><code>log</code></a> calls will include the list of tags introduced here.</p>
<h5>Params</h5>
<ul>
<li><a name="set_tags.tags"></a><a href="#tags"><code>tags</code></a>: <a href="#tags"><a href="#tags"><code>tags</code></a></a></li>
</ul>
<h4><a name="log"></a><code>log: func</code></h4>
<p>Emit a log message.</p>
<p>A log message has a <a href="#level"><code>level</code></a> describing what kind of message is being
sent, a string containing the message text, and an optional list of tags.</p>
<h5>Params</h5>
<ul>
<li><a name="log.level"></a><a href="#level"><code>level</code></a>: <a href="#level"><a href="#level"><code>level</code></a></a></li>
<li><a name="log.message"></a><code>message</code>: <code>string</code></li>
<li><a name="log.tags"></a><a href="#tags"><code>tags</code></a>: option&lt;<a href="#tags"><a href="#tags"><code>tags</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi_observe_metrics"></a>Import interface wasi:observe/metrics</h2>
<hr />
<h3>Types</h3>
<h4><a name="tags"></a><code>type tags</code></h4>
<p><a href="#tags"><a href="#tags"><code>tags</code></a></a></p>
<p>
----
<h3>Functions</h3>
<h4><a name="metric_increment"></a><code>metric-increment: func</code></h4>
<p>Increment a counter/gauge value.</p>
<h5>Params</h5>
<ul>
<li><a name="metric_increment.metric"></a><code>metric</code>: <code>string</code></li>
<li><a name="metric_increment.value"></a><code>value</code>: <code>f64</code></li>
<li><a name="metric_increment.tags"></a><a href="#tags"><code>tags</code></a>: option&lt;<a href="#tags"><a href="#tags"><code>tags</code></a></a>&gt;</li>
</ul>
<h4><a name="metric_set"></a><code>metric-set: func</code></h4>
<p>Set a counter/gauge value.</p>
<h5>Params</h5>
<ul>
<li><a name="metric_set.metric"></a><code>metric</code>: <code>string</code></li>
<li><a name="metric_set.value"></a><code>value</code>: <code>f64</code></li>
<li><a name="metric_set.tags"></a><a href="#tags"><code>tags</code></a>: option&lt;<a href="#tags"><a href="#tags"><code>tags</code></a></a>&gt;</li>
</ul>
<h4><a name="metric_record"></a><code>metric-record: func</code></h4>
<p>Observe histogram/summary value.</p>
<h5>Params</h5>
<ul>
<li><a name="metric_record.metric"></a><code>metric</code>: <code>string</code></li>
<li><a name="metric_record.value"></a><code>value</code>: <code>f64</code></li>
<li><a name="metric_record.tags"></a><a href="#tags"><code>tags</code></a>: option&lt;<a href="#tags"><a href="#tags"><code>tags</code></a></a>&gt;</li>
</ul>
<h2><a name="wasi_observe_tracing"></a>Import interface wasi:observe/tracing</h2>
<hr />
<h3>Types</h3>
<h4><a name="span_info"></a><code>record span-info</code></h4>
<h5>Record Fields</h5>
<ul>
<li>
<p><a name="span_info.sampled"></a><code>sampled</code>: <code>bool</code></p>
<p>Indicates whether the span is being sampled
</li>
<li>
<p><a name="span_info.span_id"></a><code>span-id</code>: option&lt;<code>string</code>&gt;</p>
<p>The current span-id. Returns `None` if no span is active.
</li>
<li>
<p><a name="span_info.trace_id"></a><code>trace-id</code>: option&lt;<code>string</code>&gt;</p>
<p>The current trace-id. Returns `None` if no span is active.
</li>
</ul>
<hr />
<h3>Functions</h3>
<h4><a name="span_name"></a><code>span-name: func</code></h4>
<p>Set the span name.</p>
<p>Override the auto-generated span name.</p>
<h5>Params</h5>
<ul>
<li><a name="span_name.name"></a><code>name</code>: <code>string</code></li>
</ul>
<h4><a name="span_tags"></a><code>span-tags: func</code></h4>
<p>Add tags to the current span.</p>
<p>Add a list of key-value-pairs to the active span.
NOTE(lxf): This is where https://opentelemetry.io/docs/specs/semconv/ would be useful.</p>
<h5>Params</h5>
<ul>
<li><a name="span_tags.tags"></a><a href="#tags"><code>tags</code></a>: list&lt;(<code>string</code>, <code>string</code>)&gt;</li>
</ul>
<h4><a name="span_event"></a><code>span-event: func</code></h4>
<p>Add an event to the current span.</p>
<p>Record an event in the active span.</p>
<h5>Params</h5>
<ul>
<li><a name="span_event.name"></a><code>name</code>: <code>string</code></li>
<li><a name="span_event.payload"></a><code>payload</code>: <code>string</code></li>
</ul>
<h4><a name="span_error"></a><code>span-error: func</code></h4>
<p>Add an error to the current span.</p>
<p>Record an error in the active span. Unlike <a href="#span_exit"><code>span-exit</code></a>, this does not end the span.
NOTE(lxf): This is where a 'shared wasi error interface' would be useful.</p>
<h5>Params</h5>
<ul>
<li><a name="span_error.error"></a><code>error</code>: <code>string</code></li>
</ul>
<h4><a name="span_exit"></a><code>span-exit: func</code></h4>
<p>Exit the current span.</p>
<p>Early-finalize the span with o11y host.
The o11y host automatically finalizes spans when they are dropped, but this function allows for explicit finalization.
This is helpful in any situation where a developer wishes for there to be no other interpretation of a span other than “successful”.</p>
<h4><a name="span_status"></a><code>span-status: func</code></h4>
<p>Get information about the current span.</p>
<p>Retrieve contextual information about the current span.</p>
<h5>Return values</h5>
<ul>
<li><a name="span_status.0"></a> <a href="#span_info"><a href="#span_info"><code>span-info</code></a></a></li>
</ul>
