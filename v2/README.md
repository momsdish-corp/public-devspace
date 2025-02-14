
# Simple Web Test

Example of text.xml

```yaml
baseURL: https://example.com
waitBeforeExit: 5
debug: true
plugins:
  reload:
    - path: /
      count: 3
      timeout: 10
      interval: 2
  require:
    # By default, this will expect status code 200
    - path: /
      timeout: 2
      statusCode: 200
      cssSelector:
        - 'title:text("Example Domain")'
        - 'body'
      antiCssSelector:
        - 'title:text("Random name")'
    # Check for a specific status code & title of the page
    - path: /404
      statusCode: 404
  performance:
    - path: /
      timeout: 5
      count: 1
      statusCode: 200
      performanceBudget:
        ttfb: 1000
        domInteractive: 2000
        domContentLoaded: 3000
        load: 4000
```

Run `devspace test ./test.yaml` to perform the test.