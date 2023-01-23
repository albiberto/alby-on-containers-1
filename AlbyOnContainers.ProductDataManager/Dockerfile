FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["AlbyOnContainers.ProductDataManager/AlbyOnContainers.ProductDataManager.csproj", "AlbyOnContainers.ProductDataManager/"]
RUN dotnet restore "AlbyOnContainers.ProductDataManager/AlbyOnContainers.ProductDataManager.csproj"
COPY . .
WORKDIR "/src/AlbyOnContainers.ProductDataManager"
RUN dotnet build "AlbyOnContainers.ProductDataManager.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AlbyOnContainers.ProductDataManager.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AlbyOnContainers.ProductDataManager.dll"]
