
/**
 * Quantumult X 随机 User-Agent 脚本
 */

let headers = $request.headers;

// 1. 定义 UA 池（包含不同设备和系统版本）
const uaPool = [
    "Mozilla/5.0 (iPhone; CPU iPhone OS 17_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Mobile/15E148 Safari/604.1",
    "Mozilla/5.0 (iPad; CPU OS 17_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/17.4 Mobile/15E148 Safari/604.1",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36",
    "Mozilla/5.0 (Linux; Android 14; Pixel 8) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Mobile Safari/537.36",
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36"
];

// 2. 随机抽取一个 UA
const randomUA = uaPool[Math.floor(Math.random() * uaPool.length)];

// 3. 强制覆盖现有的 User-Agent
// 使用 Object.keys 循环处理以确保兼容不同大小写的 key (如 user-agent)
Object.keys(headers).forEach(key => {
    if (key.toLowerCase() === 'user-agent') {
        delete headers[key];
    }
});
headers['User-Agent'] = randomUA;

// 4. 日志记录：方便在 Quantumult X 里的 "最近请求" 中确认效果
console.log(`[Random-UA] 随机结果: ${randomUA}`);

$done({ headers });
