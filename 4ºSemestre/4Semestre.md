# 4° Semestre • 2023-2
## Local Tracker - Sistema de Geolocalização

<p align="center">
  <img src="https://github.com/user-attachments/assets/54943760-4003-44e1-a4aa-a9bb536bf6bc" width="780" height="220" alt="Local Tracker">
</p>

**Parceiro Acadêmico:** [ITO1](https://ito1.com.br/)

## 📝 Sobre
Solução para registro e consulta de geolocalização de dispositivos, ativos e objetos em banco de dados relacional escalável e de alta disponibilidade, desenvolvida para a ITO1 (especialista em IoT).

## 🛠️ Tecnologias Utilizadas
| Área         | Tecnologias                                                                 |
|--------------|----------------------------------------------------------------------------|
| **Backend**  | Java, Spring Boot                                                          |
| **Frontend** | React, JavaScript, HTML5, CSS3                                             |
| **Banco**    | PostgreSQL                                                                 |
| **Infra**    | Docker                                                                     |
| **APIs**     | Google Maps API                                                            |

## 👨‍💻 Contribuições Pessoais

### 🔍 Sistema de Filtros Avançados
Implementação completa do sistema de filtragem:
- Filtro por intervalo de datas
- Filtro por períodos pré-definidos (hoje, semana, mês)
- Filtro combinado por tipo de dispositivo + localização

```java
@RestController
@RequestMapping("/api/locations")
public class LocationController {
    
    @GetMapping
    public ResponseEntity<List<Location>> filterLocations(
        @RequestParam(required = false) String deviceId,
        @RequestParam(required = false) @DateTimeFormat(iso = ISO.DATE) LocalDate startDate,
        @RequestParam(required = false) @DateTimeFormat(iso = ISO.DATE) LocalDate endDate) {
        
        // Lógica de filtragem
        List<Location> results = locationService.findByFilters(deviceId, startDate, endDate);
        return ResponseEntity.ok(results);
    }
}
```

### 🗺️ Integração com Google Maps API
- Renderização de dispositivos como marcadores customizados

- Desenho de áreas geofence (polígonos)

- Visualização de histórico de rotas

- Tooltips interativos

```javascript
import { GoogleMap, Marker, Polygon } from '@react-google-maps/api';

function DeviceMap({ devices, areas }) {
  return (
    <GoogleMap
      zoom={12}
      center={defaultCenter}
      mapContainerStyle={mapStyle}
    >
      {devices.map(device => (
        <Marker
          key={device.id}
          position={device.position}
          icon={customIcon}
        />
      ))}
      
      {areas.map(area => (
        <Polygon
          paths={area.coordinates}
          options={polygonOptions}
        />
      ))}
    </GoogleMap>
  );
}
```

### ⚠️ Sistema de Monitoramento Geofence
- Algoritmo ray-casting para detecção de saída de áreas

- Notificações em tempo real via WebSocket

- Dashboard de alertas

```java
@Service
public class GeofenceService {
    
    public boolean checkDeviceInArea(Device device, GeofenceArea area) {
        // Implementação do algoritmo ray-casting
        int intersections = 0;
        List<Point> vertices = area.getVertices();
        
        for (int i = 0; i < vertices.size(); i++) {
            Point v1 = vertices.get(i);
            Point v2 = vertices.get((i + 1) % vertices.size());
            
            if (rayIntersectsEdge(device.getLocation(), v1, v2)) {
                intersections++;
            }
        }
        
        return (intersections % 2) == 1;
    }
    
    private boolean rayIntersectsEdge(Point point, Point v1, Point v2) {
        // Lógica de interseção
    }
}
```

## 📈 Aprendizados

## 🧠 Hard Skills  

| Habilidade               | Nível        | Por que foi importante? |
|--------------------------|--------------|-------------------------|
| **Desenvolvimento Java** <br>(Spring Boot, JPA, Hibernate) | Avançado | Construção de APIs robustas e escaláveis para sistemas corporativos.|
| **Sistemas Geoespaciais** <br>(Geofencing, Google Maps API) | Intermediário | Processamento eficiente de dados locacionais para decisões em tempo real. |
| **React** <br>(Hooks, API Integration) | Intermediário | Criação de interfaces dinâmicas com alta responsividade. | 
| **WebSockets** | Básico | Comunicação bidirecional para atualizações instantâneas. |

---

## 💡 Soft Skills  

| Habilidade               | Por que foi importante? |
|--------------------------|-------------------------|
| **Trabalho em Equipe** | Alinhamento de times multidisciplinares em projetos complexos. | 
| **Resolução de Problemas** | Eliminação de gargalos críticos em sistemas geoespaciais. | 
| **Gestão de Tempo** | Garantia de entregas em sprints curtos sem sacrificar qualidade. | 
| **Comunicação** | Tradução de conceitos técnicos para decisores estratégicos. |
