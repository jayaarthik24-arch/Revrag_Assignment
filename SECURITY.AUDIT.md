## Decision Questions

> These questions have no single correct answer. We're evaluating how you reason through a problem, not whether you've memorised a fact.

**Q1 — Vulnerability management**

Your Trivy scan finds 3 CRITICAL CVEs in the base image. The CVEs are in OpenSSL. However, switching to a newer base image breaks one of your app's native modules. You can't fix it in the next 24 hours. What are your options and what would you actually do?

*Hint: consider the difference between fixing, mitigating, and accepting risk — and how you'd communicate your decision.*
Answer:  We identified CRITICAL OpenSSL vulnerabilities. The secure fix is to upgrade the base image, but this breaks a native module. 
          We are prioritizing a patch, but it will take longer than 24 hours to stabilize.
          Meanwhile we ensure the monitoring and alerts are in place with upgraded timelines.
          As a mitigation, we’ve restricted container privileges, tightened network access.
          we have documented the risk, communicated clearly to stakeholders, and set a remediation timeline.




---

**Q2 — Container security**

A colleague argues: *"We use* `*--privileged*` *in Docker, but it's fine because this service is only ever accessed internally, never from the internet."* How do you respond? Be specific about *what* the risk is, not just that it's bad.

Answer: I would start by explaining the collegue that "--privileged gives the container full root-level access to the host, bypassing most of Docker’s isolation mechanisms. 
        The container can access kernel and all the devices on the host which means the container is no longer sandboxed.
        The internal networks have equal risk to get compromised and if any hacker gains access (through a bug, malicious dependency, or even an insider mistake) to an internal service and the privileged container could be explout.
        So whoever may have access or not at the moment to the container, but being exposed to the vulnerability is always a threat and taking precaution is better than troubleshooting later.
        

---

**Q3 — Git history & secrets**

You've removed the hardcoded secrets from the YAML file and rotated the credentials. Your manager says "great, we're clean now." Is that true? If not — what else needs to happen, and why?

*Hint: Think about what git commits preserve, and for how long.*
Answer: Removing hardcoded secrets may not be enough as the history still remains in the commits. It would be wise to purge the history by using force push
        Also we need to make sure that the branch or the code wasn't cloned anywhere with the credentials on it. 
        It is adviseable to utilize the Github secrets or vaults provided by the cloud companies to store sensitive info like secrets.


---

**Q4 — Trade-off reasoning**

You want to pin all GitHub Actions to commit SHAs for supply chain security. Your teammate says this makes updating dependencies a pain. What's a practical approach that gives you both security and maintainability?
Answe: Pinning helps to ensure that we run the exact code that is been audited. But pinning only SHAs makes it really hectic. Instead, we can reference the version tag with the SHA commit.
       We can setup an automated workflow to check for new releases of critical anctions
       And the logs can be audited regularly. Use GitHub’s Dependabot or similar tools to alert you when a new version of an action is released. This way we get supply chain security without sacrificing maintainability.
