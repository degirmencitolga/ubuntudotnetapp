FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 5053

ENV ASPNETCORE_URLS=http://+:5053

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["finaldotnetproject.csproj", "./"]
RUN dotnet restore "finaldotnetproject.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "finaldotnetproject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "finaldotnetproject.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "finaldotnetproject.dll"]
