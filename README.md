import requests

class IOCScanner:
    def __init__(self, ioc_list):
        self.ioc_list = ioc_list

    def scan(self):
        results = []
        for ioc in self.ioc_list:
            result = self._query_ioc(ioc)
            if result:
                results.append(result)
        return results

    def _query_ioc(self, ioc):
        url = f"https://example.com/query?ioc={ioc}"
        response = requests.get(url)
        if response.status_code == 200:
            data = response.json()
            if data.get('matches'):
                return f"IOC {ioc} matched: {data['matches']}"
        return None

# 示例用法
ioc_list = ['example1', 'example2', 'example3']
scanner = IOCScanner(ioc_list)
results = scanner.scan()
for result in results:
    print(result)
