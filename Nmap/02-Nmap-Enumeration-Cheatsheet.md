# Nmap Enumeration Cheatsheet

## Host Discovery

```bash
nmap <IP>
```

## Service & Version Detection

```bash
nmap -sV <IP>
```

## Default NSE Scripts

```bash
nmap -sC <IP>
```

## Common Scan

```bash
nmap -sC -sV <IP>
```

## Aggressive Scan

```bash
nmap -A <IP>
```

## All TCP Ports

```bash
nmap -p- <IP>
```

## Faster Scan

```bash
nmap -Pn --min-rate 1000 <IP>
```

## Save Output

```bash
nmap -oA scan <IP>
```

## Enumeration Workflow

1. Discover host.
2. Scan all ports.
3. Detect services & versions.
4. Run default NSE scripts.
5. Enumerate discovered services.

## Key Takeaways

- Enumerate before exploiting.
- Scan all ports when necessary.
- Verify findings manually.
- Build an attack path.
