# Optional YEScale real-model setup

The public practice run uses the offline mock model and needs no API key.
The real-model path reads three environment variables directly; it does not
load a `.env` file.

In PowerShell, set the endpoint and model for the current terminal:

```powershell
$env:ARENA_BASE_URL = "https://api.yescale.io/v1"
$env:ARENA_MODEL = "gpt-4o-mini"
```

When a real-model run is needed, enter your own key without putting it in a
file or shell history:

```powershell
$secret = Read-Host "YEScale API key" -AsSecureString
$env:ARENA_API_KEY = [System.Net.NetworkCredential]::new("", $secret).Password
Remove-Variable secret
.\.venv\Scripts\python.exe scripts/run_practice.py --model real
```

The endpoint comes from [YEScale's example](https://yescale.io/), which uses
`/v1/chat/completions`. `arena/model.py` appends `/chat/completions` to
`ARENA_BASE_URL`. Check that your YEScale account provides the chosen model.
Never commit a key or a real-run transcript containing sensitive input.
