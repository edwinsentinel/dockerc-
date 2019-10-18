FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["dockersampleCsharp/dockersampleCsharp.csproj", "dockersampleCsharp/"]
RUN dotnet restore "dockersampleCsharp/dockersampleCsharp.csproj"
COPY . .
WORKDIR "/src/dockersampleCsharp"
RUN dotnet build "dockersampleCsharp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "dockersampleCsharp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dockersampleCsharp.dll"]