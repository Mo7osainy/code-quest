FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /src

COPY ["Worker.csproj", "."]

RUN dotnet restore "Worker.csproj"

COPY . .

RUN dotnet publish -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/runtime:7.0

RUN adduser --disabled-password --gecos '' --shell /bin/false --uid 1001 workeruser

WORKDIR /app

COPY --from=build --chown=workeruser:workeruser /app/publish .

USER workeruser

CMD ["dotnet", "Worker.dll"]
