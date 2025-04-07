# Infra-Devops-portfolio

Este repositório demonstra o uso básico de ferramentas essenciais de DevOps: **GitHub Actions, AWS, Terraform e Ansible**.

---

## Estrutura do projeto
```
infra-devops-portfolio/
├── .github/
│ └── workflows/
│ └── ci.yml # Pipeline automatizado com GitHub Actions
├── ansible/
│ ├── hosts # Inventário de hosts
│ └── playbook.yml # Playbook para instalar o Nginx
├── terraform/
│ └── main.tf # Criação de instância EC2 na AWS
├── scripts/
│ └── hello.sh # Script simples chamado pelo pipeline
└── README.md
```

---

## 1. GitHub Actions (`.github/workflows/ci.yml`)
```yaml
name: CI Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout código
        uses: actions/checkout@v3

      - name: Rodar script
        run: bash scripts/hello.sh
```

---

## 2. AWS + Terraform (`terraform/main.tf`)
```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "exemplo" {
  ami = "ami-0c55b159cbfafe1f0" # Substitua pela AMI válida da sua região
  instance_type = "t2.micro"
  tags = {
    Name = "Exemplo-Instance"
  }
}
```

---

## 3. Ansible
### hosts (ansible/hosts)
```
[servidores]
192.168.0.10 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/minhachave.pem
```

### playbook.yml (ansible/playbook.yml)
```yaml
- name: Instalar Nginx
  hosts: servidores
  become: yes
  tasks:
    - name: Instala nginx
      apt:
        name: nginx
        state: present
```

---

## 4. Script de exemplo (`scripts/hello.sh`)
```bash
#!/bin/bash
echo "Pipeline funcionando!"
```

---

## Como rodar tudo:

### Terraform:
```bash
cd terraform
terraform init
terraform apply
```

### Ansible:
```bash
cd ansible
ansible-playbook -i hosts playbook.yml
```

### GitHub Actions:
- Faça push para a branch `main` e observe o pipeline rodar automaticamente na aba "Actions" do repositório.

---

Com esse projeto, demonstro conhecimento prático no ciclo completo de provisionamento, automação e CI/CD. Pronto para evoluir e integrar soluções reais!



