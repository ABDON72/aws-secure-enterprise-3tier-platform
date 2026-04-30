## Key Features
- High availability across 2 Availability Zones
- Auto Scaling — automatically replaces unhealthy instances
- WAF protection — blocks XSS and SQL injection attacks
- Zero hardcoded credentials — IAM roles only
- Complete audit trail via CloudTrail
- Compliance monitoring with AWS Config

## Implementation Steps
- Step 1: VPC with public/private subnets across 2 AZs
- Step 2: Security groups with least privilege
- Step 3: Launch Template with Nginx auto-install script
- Step 4: Application Load Balancer and Target Group
- Step 5: Auto Scaling Group with health checks
- Step 6: RDS MySQL in private subnets
- Step 7: WAF with managed rule sets
- Step 8: CloudWatch alarms, CloudTrail, AWS Config

## Security Architecture
- EC2 instances in private subnets — no public IP
- ALB only accepts traffic from WAF
- RDS only accepts traffic from EC2 security group
- IAM roles — no hardcoded AWS credentials
- MFA enabled on root account
- SSH restricted to specific IP only

## CloudWatch Alarms
| Alarm | Condition |
|---|---|
| High CPU | CPUUtilization > 50% |
| ALB Errors | HTTPCode_Target_4XX_Count > 10 |
| Unhealthy Targets | UnHealthyHostCount >= 1 |
| RDS Low Storage | FreeStorageSpace < 1GB |
| High Latency | TargetResponseTime > 2 seconds |

## AWS Config Compliance Results
| Rule | Status |
|---|---|
| restricted-ssh | Compliant ✅ |
| rds-instance-public-access-check | Compliant ✅ |
| root-account-mfa-enabled | Compliant ✅ |
| s3-bucket-public-read-prohibited | Compliant ✅ |
| encrypted-volumes | Noncompliant ⚠️ |

## Testing Results
| Test | Result |
|---|---|
| Website loads through ALB | PASS ✅ |
| WAF blocks XSS attack | PASS ✅ (403 Forbidden) |
| Auto Scaling self-healing | PASS ✅ |
| CloudTrail logging | PASS ✅ |
| Config compliance | PASS ✅ (4/5 rules) |

## Known Findings & Remediation Plan
| Finding | Severity | Remediation |
|---|---|---|
| EBS volumes unencrypted | High | Create encrypted snapshots, copy with KMS encryption, replace existing volumes |

## Technologies
AWS EC2 · ALB · Auto Scaling · RDS MySQL · VPC · WAF · 
Shield · IAM · CloudWatch · CloudTrail · AWS Config · 
NAT Gateway · Systems Manager

## Author
Abdon Njunwa
- GitHub: [@ABDON72](https://github.com/ABDON72)
- Certifications: CompTIA A+ | CompTIA Security+
