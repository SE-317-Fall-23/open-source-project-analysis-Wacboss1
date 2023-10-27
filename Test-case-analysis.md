# Assignment Submission

## Project Selected: Flask

## I. Introduction
- Briefly introduce the purpose of this section, which is to provide a detailed description of two test cases in the selected open-source project.

## II. Test Case 1: test_options_work
### A. Description
- This test is used to check that only the set http options are allowed
### B. Gherkin Syntax (if applicable)
  Given a new flask app<br/>
  And a client<br/>
  When the methods are set to Get and Post<br/>
  Then the allowed methods are Get, Post, Head, and Options<br/>
  And there is no data in the response
### C. Test Steps
<ol>
<li>Create a route at path "/" that accepts only accepts Get and Post request</li>
<li>Use the client to open the request at "/"</li>
<li>Assert that the list of allowed options only includes GET, HEAD, OPTIONS, and POST</li>
<li>Assert that there is no data in the response</li>
</ol>

### D. Code Segments Under Test
- Identify specific code segments or functions that are being tested in this case.

```python
def dispatch_request(self) -> ft.ResponseReturnValue:
        """Does the request dispatching.  Matches the URL and returns the
        return value of the view or error handler.  This does not have to
        be a response object.  In order to convert the return value to a
        proper response object, call :func:`make_response`.

        .. versionchanged:: 0.7
           This no longer does the exception handling, this code was
           moved to the new :meth:`full_dispatch_request`.
        """
        req = request_ctx.request
        if req.routing_exception is not None:
            self.raise_routing_exception(req)
        rule: Rule = req.url_rule  # type: ignore[assignment]
        # if we provide automatic options for this URL and the
        # request came with the OPTIONS method, reply automatically
        if (
            getattr(rule, "provide_automatic_options", False)
            and req.method == "OPTIONS"
        ):
            return self.make_default_options_response()
        # otherwise dispatch to the handler for that endpoint
        view_args: dict[str, t.Any] = req.view_args  # type: ignore[assignment]
        return self.ensure_sync(self.view_functions[rule.endpoint])(**view_args)
```
```python
def make_default_options_response(self) -> Response:
        """This method is called to create the default ``OPTIONS`` response.
        This can be changed through subclassing to change the default
        behavior of ``OPTIONS`` responses.

        .. versionadded:: 0.7
        """
        adapter = request_ctx.url_adapter
        methods = adapter.allowed_methods()  # type: ignore[union-attr]
        rv = self.response_class()
        rv.allow.update(methods)
        return rv
```

### E. Initial State
- App with a route at "/" that should only accept methods GET and POST
### F. Transition
- A client sends a request to path "/"
### G. Expected State
- The responce should tell the client that only GET,POST, HEAD, and OPTIONS methods are avaliable

## III. Test Case 2: test_method_route_no_methods
### A. Description
- This test check that if a route does not have a method, an error is thrown
### B. Gherkin Syntax (if applicable)
- Given a app with a route
- When no method is present for that route
- Then a typeError is thrown
### C. Test Steps
<ol>
    <li>Try to execute app.get with no corresponding method</li>
    <li>Assert where a typeError is raised</li>
</ol>

### D. Code Segments Under Test
- Identify specific code segments or functions that are being tested in this case.
```python
def _method_route(
        self,
        method: str,
        rule: str,
        options: dict,
    ) -> t.Callable[[T_route], T_route]:
        if "methods" in options:
            raise TypeError("Use the 'route' decorator to use the 'methods' argument.")

        return self.route(rule, methods=[method], **options)
```
### E. Initial State
- App with no methods
### F. Transition
- there is no change is state becuase this test is checking for a failed setup of state
### G. Expected State
- TypeError is thrown

