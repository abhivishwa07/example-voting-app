FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:7.0 AS build
ARG TARGETARCH
WORKDIR /source

COPY src/Worker/*.csproj .
RUN dotnet restore -a "$TARGETARCH"

COPY src/Worker/ .
RUN dotnet publish -c release -o /app -a "$TARGETARCH" --no-restore

# runtime image
FROM mcr.microsoft.com/dotnet/runtime:7.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Worker.dll"]