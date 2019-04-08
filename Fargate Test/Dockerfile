FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Fargate Test/Fargate Test.csproj", "Fargate Test/"]
RUN dotnet restore "Fargate Test/Fargate Test.csproj"
COPY . .
WORKDIR "/src/Fargate Test"
RUN dotnet build "Fargate Test.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Fargate Test.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Fargate Test.dll"]