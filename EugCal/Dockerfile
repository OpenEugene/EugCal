FROM codegold79/mvpstudio-dotnet:v1 as base
FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["EugCal.csproj", ""]
COPY ["NuGet.Config", "/root/.nuget/NuGet/NuGet.Config"]
RUN dotnet restore "./EugCal.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "EugCal.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EugCal.csproj" -c Release -o /app/publish

FROM base AS final
USER mvp
WORKDIR /home/mvp/app
COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "EugCal.dll"]
