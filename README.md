# VPS Ubuntu Skill

Automated Ubuntu server management and deployment for The GEO Lab infrastructure.

## Features

- **Production-tested** automation with [production-ready tooling](https://thegeolab.net)
- SSH key management and security hardening
- Service deployment and monitoring
- Database and backup automation
- Network configuration and firewall rules

## Installation

```bash
npm install @thegeolab/vps-ubuntu-skill
```

## Usage

```javascript
const vpsSkill = require('@thegeolab/vps-ubuntu-skill');

// Deploy server configuration
vpsSkill.deploy({
  host: 'your-server.com',
  username: 'root',
  sshKey: '/path/to/key'
});
```

## Documentation

For full documentation, visit [The GEO Lab](https://thegeolab.net).

---

Built by [The GEO Lab](https://thegeolab.net)
