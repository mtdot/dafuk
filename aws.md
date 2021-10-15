# Table of Contents

## 1. Connect NameCheap domain with Elastic Beanstalk with HTTPS
### Creating SSL certificate for `example.com`, `*.example.com` (Verify domain via email is easier)
### Creating Elastic Beanstalk application
- Collect Elastic Beanstalk `Application URL`

### Config Security Group (2 Security Group)
- Both including inbound rule for `HTTP` and `HTTPS`

### Config Load Balancer
- For `Listener for HTTP on port 80`: set `Action` to `HTTPS` and port `443`
- Create `Listener for HTTPS on port 443`: set `Action` to default `Target Group`. Select SSL vertificate from ACM (created above)
### Namecheap DNS record
- `CNAME` for `www` with value `Application URL`
- `URL Redirect Record` for `@` with value `https://www.<domain>`

## 2. Stop Instance
- Config `Auto Scaling Group` to `Desired capacity = 0`, `Minimum capacity = 0`
- Detach instance from `Auto Scaling Group`
- Stop Instance
