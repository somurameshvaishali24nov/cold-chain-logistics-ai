# Ingesting Data

- Download the dataset from 'data.txt'
- Create an EC2 Instance > docker container > mcr,microsoft.com/mssql/server:2022-latest

docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=FdeEnterprisePass123!" -p 1433:1433 --name legacy-mssql -d mcr.microsoft.com/mssql/server:2022-latest

docker run -v mssql_data:/var/opt/mssql \
    -e "ACCEPT_EULA=Y" \
    -e "MSSQL_SA_PASSWORD=FdeEnterprisePass123!" \
    -p 1433:1433 \
    --name legacy-mssql \
    -d mcr.microsoft.com/mssql/server:2022-latest


```
rm -rf .venv
uv init --bare --python 3.12
grep -vE '^(torch|sentence-transformers|langchain-huggingface)==' requirement.txt > /tmp/req.txt
uv add -r /tmp/req.txt
uv run python --version

rm -rf .venv
uv python pin 3.12
sed -i '' 's/^requires-python.*/requires-python = ">=3.12,<3.13"/' pyproject.toml
uv sync
uv run python --version

which python            # should end in .../Cold-Chain_Logistics_AI/.venv/bin/python
python --version        # should be 3.12.x
echo $VIRTUAL_ENV       # prints the .venv path if it's active

uv run python --version
uv run main.py

source .venv/bin/activate
deactivate              
```