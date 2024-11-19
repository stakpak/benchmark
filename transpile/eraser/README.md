# Terraform Diagram Conversion Benchmarking: Stakpak vs OpenAI o1-preview

## Detailed Performance Comparison

| Example | Stakpak Time | OpenAI o1-preview Time | Stakpak Cost | OpenAI o1-preview Cost |
|---------|--------------|------------------------|--------------|------------------------|
| 1: EKS Module | 25.281s | 67.541s | $0.001678 | $0.59 |
| 2: AWS Nextjs | 11.146s | 61.910s | $0.001023 | $0.45 |
| 3: Lambda Module | 18.781s | 85.550s | $0.001921 | $0.72 |
| 4: Route53 Resolver | 4.918s | 104.331s | $0.000515 | $0.52 |

## Performance Analysis

### Speed Comparison
- **Example 1 (EKS Module)**: Stakpak 2.67x faster
- **Example 2 (AWS Nextjs)**: Stakpak 5.56x faster
- **Example 3 (Lambda Module)**: Stakpak 4.56x faster
- **Example 4 (Route53 Resolver)**: Stakpak 21.23x faster

### Cost Comparison
- **Example 1 (EKS Module)**: Stakpak 352.8x cheaper
- **Example 2 (AWS Nextjs)**: Stakpak 439.9x cheaper
- **Example 3 (Lambda Module)**: Stakpak 374.7x cheaper
- **Example 4 (Route53 Resolver)**: Stakpak 1009.7x cheaper

## Overall Conclusion

Stakpak is 8.5x faster and 544x cheaper than OpenAI o1-preview in Terraform diagram conversion across multiple AWS infrastructure module examples.