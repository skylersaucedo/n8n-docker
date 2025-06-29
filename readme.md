# n8n Docker Environment with MCP Support

A complete Docker-based setup for running n8n workflow automation platform with Model Context Protocol (MCP) client support. This repository provides multiple deployment options from simple SQLite setups to production-ready PostgreSQL configurations with comprehensive MCP integration.

## 🚀 Quick Start

```bash
# Clone or download the files
git clone <your-repo-url>
cd n8n-docker-mcp

# Start with basic SQLite setup
docker-compose up -d

# Access n8n
open http://localhost:5678
```

## 📋 What's Included

- **Multiple Docker Compose configurations** (SQLite & PostgreSQL)
- **Pre-configured MCP environment variables** for popular services
- **Custom Dockerfile** for advanced customizations
- **Comprehensive setup guides** and troubleshooting
- **Production-ready configurations** with security best practices

## 🏗️ Project Structure

```
├── docker-compose.yml              # Basic setup with SQLite
├── docker-compose-postgres.yml     # Production setup with PostgreSQL
├── Dockerfile                      # Custom Docker image (optional)
├── README.md                       # This file
├── docs/
│   ├── setup-instructions.md       # Detailed setup guide
│   └── mcp-setup-guide.md         # MCP configuration guide
└── .env.example                    # Environment variables template
```

## 🐳 Deployment Options

### Option 1: Basic Setup (SQLite)
**Best for**: Development, testing, small workloads

```bash
docker-compose up -d
```

**Features**:
- SQLite database (file-based)
- MCP client support enabled
- Timezone configured for US Central
- Data persistence via Docker volumes

### Option 2: Production Setup (PostgreSQL)
**Best for**: Production environments, team usage, high workloads

```bash
docker-compose -f docker-compose-postgres.yml up -d
```

**Features**:
- PostgreSQL database
- Health checks and dependencies
- Encryption key configuration
- Scalable architecture

### Option 3: Custom Build
**Best for**: Custom requirements, additional packages

```bash
docker build -t my-n8n .
docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n my-n8n
```

## 🤖 MCP (Model Context Protocol) Integration

This setup includes full support for MCP, enabling your n8n workflows to interact with external tools and AI services.

### Pre-configured MCP Servers

| Service | Environment Variable | Purpose |
|---------|---------------------|---------|
| Brave Search | `MCP_BRAVE_API_KEY` | Web search capabilities |
| OpenAI | `MCP_OPENAI_API_KEY` | AI model integration |
| Serper | `MCP_SERPER_API_KEY` | Search API services |
| Weather API | `MCP_WEATHER_API_KEY` | Weather data access |

### MCP Setup Steps

1. **Install MCP Client Node**:
   ```
   Settings → Community Nodes → Install: n8n-nodes-mcp
   ```

2. **Configure API Keys**:
   ```yaml
   # Uncomment in docker-compose.yml
   - MCP_BRAVE_API_KEY=your-api-key-here
   ```

3. **Create MCP Credentials** in n8n interface

4. **Build AI Agents** using MCP tools

## ⚙️ Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `N8N_HOST` | `localhost` | n8n host address |
| `N8N_PORT` | `5678` | n8n port |
| `GENERIC_TIMEZONE` | `America/Chicago` | Application timezone |
| `N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE` | `true` | Enable MCP tools |

### Security Configuration

**Important**: For production deployments:

1. **Change the encryption key**:
   ```yaml
   - N8N_ENCRYPTION_KEY=your-very-secure-encryption-key-change-this
   ```

2. **Update database passwords**:
   ```yaml
   - DB_POSTGRESDB_PASSWORD=secure-password-here
   ```

3. **Configure proper networking** and firewall rules

## 📊 Monitoring & Maintenance

### Health Checks
Both configurations include health checks:
- PostgreSQL: `pg_isready` check
- n8n: HTTP endpoint monitoring

### Updating n8n
```bash
# Pull latest images
docker-compose pull

# Restart with new version
docker-compose up -d
```

### Backup & Restore
```bash
# Backup volumes
docker run --rm -v n8n_data:/data -v $(pwd):/backup alpine tar czf /backup/n8n-backup.tar.gz /data

# Restore volumes
docker run --rm -v n8n_data:/data -v $(pwd):/backup alpine tar xzf /backup/n8n-backup.tar.gz -C /
```

## 🛠️ Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| Port 5678 in use | Change to `-p 8080:5678` |
| MCP tools not available | Ensure `N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE=true` |
| Database connection fails | Check PostgreSQL health status |
| Permission errors | Verify Docker permissions |

### Logs
```bash
# View n8n logs
docker-compose logs -f n8n

# View all service logs
docker-compose logs -f
```

### Debug Mode
```bash
# Start with debug logging
docker-compose up -d
docker-compose exec n8n n8n start --verbose
```

## 🔧 Customization

### Adding Custom Packages
Modify the `Dockerfile`:
```dockerfile
# Switch to root for package installation
USER root
RUN apk add --no-cache git curl
USER node
```

### Custom Environment Variables
Create `.env` file:
```bash
N8N_HOST=0.0.0.0
N8N_ENCRYPTION_KEY=my-secret-key
MCP_BRAVE_API_KEY=my-api-key
```

Use in docker-compose:
```yaml
env_file:
  - .env
```

## 📚 Documentation

- [Setup Instructions](docs/setup-instructions.md) - Detailed deployment guide
- [MCP Setup Guide](docs/mcp-setup-guide.md) - Complete MCP configuration
- [n8n Official Docs](https://docs.n8n.io/) - n8n documentation
- [MCP Protocol Docs](https://modelcontextprotocol.io/) - MCP specification

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### Development Setup
```bash
# Clone repository
git clone <repo-url>
cd n8n-docker-mcp

# Start development environment
docker-compose up -d

# Make changes and test
docker-compose restart n8n
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Issues**: [GitHub Issues](https://github.com/your-username/n8n-docker-mcp/issues)
- **n8n Community**: [n8n Community Forum](https://community.n8n.io/)
- **MCP Support**: [MCP GitHub Repository](https://github.com/nerding-io/n8n-nodes-mcp)

## 🏷️ Tags

`n8n` `docker` `automation` `workflow` `mcp` `ai` `postgres` `sqlite` `docker-compose`

---

## 🚀 Getting Started Checklist

- [ ] Clone/download this repository
- [ ] Choose deployment option (SQLite or PostgreSQL)
- [ ] Configure environment variables
- [ ] Start Docker containers
- [ ] Access n8n at http://localhost:5678
- [ ] Install MCP client node
- [ ] Configure MCP credentials
- [ ] Create your first workflow
- [ ] Build AI agents with MCP tools

**Happy Automating! 🎉**