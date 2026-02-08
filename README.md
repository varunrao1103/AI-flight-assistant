# AI flight assistant 

This project was to execute open source models => gpt-oss:20B model calling tools to calculate ticket price. 

We exposed get_ticket_price() as tools to the model with destination as parameter.
As we know that gpt-oss is not capable of executing tools, we handled it handle_tool_call()

### Tool calling :
ChatCompletionMessage(content='Hello! How can I help you today?', refusal=None, role='assistant', annotations=None, audio=None, function_call=None, tool_calls=None, reasoning='User says "hey". It\'s a greeting. We respond with a greeting. No tool needed. Short, courteous, <=1 sentence.')
ChatCompletionMessage(content='', refusal=None, role='assistant', annotations=None, audio=None, function_call=None, tool_calls=[ChatCompletionMessageFunctionToolCall(id='call_xqe9l8bw', function=Function(arguments='{"destination_city":"London"}', name='get_ticket_price'), type='function', index=0)], reasoning='The user explicitly asks ticket price to London. Must call the get_ticket_price function with destination_city "London".')
DATABASE TOOL CALLED: Getting price for London
ChatCompletionMessage(content='', refusal=None, role='assistant', annotations=None, audio=None, function_call=None, tool_calls=[ChatCompletionMessageFunctionToolCall(id='call_vbg8tiyh', function=Function(arguments='{"destination_city":"London"}', name='get_ticket_price'), type='function', index=0)], reasoning='User asks: "find the ticket price to london and if the price is greater than $500 dollar, then find the ticket price to paris". This is effectively a request for ticket prices, which triggers tool use. Rules: "ONLY call a tool when user explicitly asks for ticket prices or costs." So we should call the get_ticket_price function for London. Then based on the returned price > 500, we call again for Paris. We must not mention calling tools. Also no fabrication. The tool output is unknown but we need to call.\n\nWe should call get_ticket_price for London. Then if price > 500, call for Paris. Provide answers accordingly. We\'ll do step-by-step internal calls.\n\nFirst call: get_ticket_price("London").')
DATABASE TOOL CALLED: Getting price for London
DATABASE TOOL CALLED: Getting price for Paris
