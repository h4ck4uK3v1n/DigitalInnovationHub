## Escaneo de Detección de Servicios y Sistema Operativo con Resolución de Nombres DNS en <IP_DEL_OBJETIVO>

Si quieres obtener el nombre de host de un objetivo usando solo `nmap` en Linux y el comando `nmap -sL` no te está devolviendo el nombre de host, entonces es probable que:

1. No haya un registro DNS inverso (PTR) configurado para esa IP.
2. El nombre de host no esté disponible públicamente a través de DNS.

Aquí tienes una alternativa para intentar obtener el nombre de host (o más información sobre el dispositivo) con `nmap`:

### Intentar con `nmap -sV --script dns-brute`

Si el objetivo está en una red pública y quieres probar una resolución de nombre más exhaustiva, puedes usar el script `dns-brute` de `nmap`, que realiza una búsqueda de subdominios y nombres de host en caso de que haya registros DNS configurados:

```bash
sudo nmap -sV --script dns-brute <IP_DEL_OBJETIVO>
```

- `-sV`: Detecta los servicios en ejecución y sus versiones.
- `--script dns-brute`: Realiza un "fuerza bruta" de DNS para encontrar nombres de host asociados con el objetivo.

### Ejemplo completo de comando

Si tienes permisos administrativos y quieres una detección completa que pueda encontrar más detalles, puedes combinar opciones así:

```bash
sudo nmap -sV -O --script dns-brute <IP_DEL_OBJETIVO>
```

- `-O`: Intenta identificar el sistema operativo.
- Este comando tardará más, pero puede proporcionar información detallada si la IP está bien configurada para resolver su nombre de host.