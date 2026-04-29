Trivy is a lightweight, fast security scanner used to find vulnerabilities (CVE) and misconfigurations (IaC) across code repositories, binary artifacts, container images, and Kubernetes clusters.

It's easy to integrate trivy with CI/CD (GitHub Actions, GitLab, etc).

---**Windows PoC** ---------------------------------------------------------------------------------

Step-by-step installation
- Download trivy_x.xx.x_windows-64bit.zip file from [releases page](https://github.com/aquasecurity/trivy/releases/).
- Unzip file and copy to any folder.
- Add trivy to the PATH system. 

Tests

- trivy in PATH system
![[Pasted image 20260429144905.png]]

- trivy --version
![[Pasted image 20260429144755.png]]

- 