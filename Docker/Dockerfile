FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["HelloWorldMvc/HelloWorldMvc.csproj", "HelloWorldMvc/"]
RUN dotnet restore "HelloWorldMvc/HelloWorldMvc.csproj"
COPY . .
WORKDIR "/src/HelloWorldMvc"
RUN dotnet build "HelloWorldMvc.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloWorldMvc.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloWorldMvc.dll"]
