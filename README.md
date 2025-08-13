 ArchitectFactory


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Manufacturing Platform - Layered Architecture</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }
        
        .header {
            text-align: center;
            margin-bottom: 40px;
            padding-bottom: 20px;
            border-bottom: 3px solid #667eea;
        }
        
        .header h1 {
            color: #2c3e50;
            font-size: 2.5em;
            margin: 0;
            font-weight: 700;
        }
        
        .header p {
            color: #7f8c8d;
            font-size: 1.2em;
            margin: 10px 0;
        }
        
        .architecture-container {
            display: flex;
            flex-direction: column;
            gap: 25px;
            margin: 30px 0;
        }
        
        .layer {
            border-radius: 15px;
            padding: 25px;
            position: relative;
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .layer:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
        }
        
        .layer-title {
            font-size: 1.8em;
            font-weight: 700;
            margin: 0 0 20px 0;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .layer-icon {
            font-size: 2em;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(255,255,255,0.2);
        }
        
        .presentation-layer {
            background: linear-gradient(135deg, #ff6b6b, #ee5a52);
            color: white;
        }
        
        .business-layer {
            background: linear-gradient(135deg, #4ecdc4, #44a08d);
            color: white;
        }
        
        .api-layer {
            background: linear-gradient(135deg, #45b7d1, #96c93d);
            color: white;
        }
        
        .data-access-layer {
            background: linear-gradient(135deg, #f7b731, #fc7b03);
            color: white;
        }
        
        .database-layer {
            background: linear-gradient(135deg, #5f27cd, #341f97);
            color: white;
        }
        
        .components-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .component-card {
            background: rgba(255,255,255,0.15);
            padding: 20px;
            border-radius: 12px;
            border: 2px solid rgba(255,255,255,0.2);
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
        }
        
        .component-card:hover {
            background: rgba(255,255,255,0.25);
            transform: scale(1.02);
        }
        
        .component-title {
            font-size: 1.3em;
            font-weight: 600;
            margin: 0 0 10px 0;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .component-description {
            font-size: 0.95em;
            opacity: 0.9;
            margin: 10px 0;
            line-height: 1.4;
        }
        
        .component-features {
            list-style: none;
            padding: 0;
            margin: 15px 0 0 0;
        }
        
        .component-features li {
            padding: 5px 0;
            font-size: 0.9em;
            opacity: 0.85;
            position: relative;
            padding-left: 20px;
        }
        
        .component-features li::before {
            content: '✓';
            position: absolute;
            left: 0;
            font-weight: bold;
            color: rgba(255,255,255,0.8);
        }
        
        .data-flow-arrows {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: -10px 0;
            z-index: 10;
            position: relative;
        }
        
        .arrow {
            font-size: 2.5em;
            color: #34495e;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            animation: bounce 2s infinite;
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }
        
        .layer-metrics {
            display: flex;
            justify-content: space-around;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid rgba(255,255,255,0.3);
        }
        
        .metric {
            text-align: center;
        }
        
        .metric-value {
            font-size: 1.5em;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .metric-label {
            font-size: 0.9em;
            opacity: 0.8;
        }
        
        .integration-lines {
            position: absolute;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }
        
        .tech-stack {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 15px;
        }
        
        .tech-badge {
            background: rgba(255,255,255,0.3);
            padding: 4px 12px;
            border-radius: 15px;
            font-size: 0.8em;
            font-weight: 500;
            border: 1px solid rgba(255,255,255,0.4);
        }
        
        .layer-number {
            position: absolute;
            top: -15px;
            left: 30px;
            background: #2c3e50;
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2em;
            font-weight: bold;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
        }
        
        @media (max-width: 768px) {
            .components-grid {
                grid-template-columns: 1fr;
            }
            
            .layer-metrics {
                flex-direction: column;
                gap: 15px;
            }
            
            .header h1 {
                font-size: 2em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Manufacturing Platform Layered Architecture</h1>
            <p>Enterprise-Scale Manufacturing System | 3,000 Facilities | 1M Users | 25M IoT Devices</p>
        </div>
        
        <div class="architecture-container">
            <!-- Layer 1: Presentation Layer -->
            <div class="layer presentation-layer">
                <div class="layer-number">1</div>
                <div class="layer-title">
                    <div class="layer-icon">🖥️</div>
                    Presentation Layer
                </div>
                
                <div class="components-grid">
                    <div class="component-card">
                        <div class="component-title">📱 Mobile Apps</div>
                        <div class="component-description">
                            Native and cross-platform mobile applications for factory workers, supervisors, and field technicians
                        </div>
                        <ul class="component-features">
                            <li>Factory worker task management</li>
                            <li>Supervisor monitoring dashboard</li>
                            <li>Real-time alerts and notifications</li>
                            <li>Offline capability for field work</li>
                            <li>Barcode/QR code scanning</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">React Native</span>
                            <span class="tech-badge">Flutter</span>
                            <span class="tech-badge">PWA</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">🖊️ Web Dashboard</div>
                        <div class="component-description">
                            Comprehensive web-based dashboards for management, analytics, and administrative functions
                        </div>
                        <ul class="component-features">
                            <li>Executive KPI dashboards</li>
                            <li>Financial reporting interfaces</li>
                            <li>Production planning tools</li>
                            <li>Quality management console</li>
                            <li>Analytics and BI visualizations</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">React</span>
                            <span class="tech-badge">Angular</span>
                            <span class="tech-badge">D3.js</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">🌐 Portals</div>
                        <div class="component-description">
                            Specialized portals for different user groups and external stakeholders
                        </div>
                        <ul class="component-features">
                            <li>Supplier collaboration portal</li>
                            <li>Customer service portal</li>
                            <li>Partner integration portal</li>
                            <li>Maintenance vendor portal</li>
                            <li>Regulatory compliance portal</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Next.js</span>
                            <span class="tech-badge">Vue.js</span>
                            <span class="tech-badge">SSO</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">🏭 IoT Devices</div>
                        <div class="component-description">
                            Connected manufacturing equipment, sensors, and embedded systems
                        </div>
                        <ul class="component-features">
                            <li>Production equipment interfaces</li>
                            <li>Environmental sensors</li>
                            <li>Safety monitoring systems</li>
                            <li>Asset tracking devices</li>
                            <li>Quality inspection tools</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">MQTT</span>
                            <span class="tech-badge">OPC-UA</span>
                            <span class="tech-badge">Modbus</span>
                        </div>
                    </div>
                </div>
                
                <div class="layer-metrics">
                    <div class="metric">
                        <div class="metric-value">500K</div>
                        <div class="metric-label">Daily Active Users</div>
                    </div>
                    <div class="metric">
                        <div class="metric-value">25M</div>
                        <div class="metric-label">Connected Devices</div>
                    </div>
                    <div class="metric">
                        <div class="metric-value">3,000</div>
                        <div class="metric-label">Facilities</div>
                    </div>
                </div>
            </div>
            
            <div class="data-flow-arrows">
                <div class="arrow">⬇</div>
            </div>
            
            <!-- Layer 2: Business Layer -->
            <div class="layer business-layer">
                <div class="layer-number">2</div>
                <div class="layer-title">
                    <div class="layer-icon">⚙️</div>
                    Business Layer
                </div>
                
                <div class="components-grid">
                    <div class="component-card">
                        <div class="component-title">🏭 Production Service</div>
                        <div class="component-description">
                            Core production management services handling orders, monitoring, and scheduling
                        </div>
                        <ul class="component-features">
                            <li>Production order management</li>
                            <li>Real-time equipment monitoring</li>
                            <li>Production scheduling optimization</li>
                            <li>Capacity planning and allocation</li>
                            <li>Performance metrics tracking</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Spring Boot</span>
                            <span class="tech-badge">Microservices</span>
                            <span class="tech-badge">Event-Driven</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">💰 Costing & Payment Service</div>
                        <div class="component-description">
                            Financial services for cost calculation, payment processing, and financial workflows
                        </div>
                        <ul class="component-features">
                            <li>Real-time cost calculation</li>
                            <li>Automated payment processing</li>
                            <li>Financial reporting and analytics</li>
                            <li>Budget management and forecasting</li>
                            <li>Invoice generation and tracking</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Node.js</span>
                            <span class="tech-badge">Payment APIs</span>
                            <span class="tech-badge">Blockchain</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">🔧 Maintenance Service</div>
                        <div class="component-description">
                            Comprehensive maintenance management with predictive analytics and workflow automation
                        </div>
                        <ul class="component-features">
                            <li>Predictive maintenance algorithms</li>
                            <li>Maintenance workflow automation</li>
                            <li>Asset lifecycle management</li>
                            <li>Technician scheduling and dispatch</li>
                            <li>Maintenance escalation procedures</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Python</span>
                            <span class="tech-badge">ML/AI</span>
                            <span class="tech-badge">TensorFlow</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">📊 Analytics & Reporting</div>
                        <div class="component-description">
                            Business intelligence and analytics services for insights and decision support
                        </div>
                        <ul class="component-features">
                            <li>Real-time business intelligence</li>
                            <li>Predictive analytics models</li>
                            <li>Custom report generation</li>
                            <li>KPI monitoring and alerting</li>
                            <li>Data visualization services</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Apache Spark</span>
                            <span class="tech-badge">Kafka Streams</span>
                            <span class="tech-badge">Apache Flink</span>
                        </div>
                    </div>
                </div>
                
                <div class="layer-metrics">
                    <div class="metric">
                        <div class="metric-value">10M</div>
                        <div class="metric-label">Daily Transactions</div>
                    </div>
                    <div class="metric">
                        <div class="metric-value">99.9%</div>
                        <div class="metric-label">Service Uptime</div>
                    </div>
                    <div class="metric">
                        <div class="metric-value">&lt;100ms</div>
                        <div class="metric-label">Response Time</div>
                    </div>
                </div>
            </div>
            
            <div class="data-flow-arrows">
                <div class="arrow">⬇</div>
            </div>
            
            <!-- Layer 3: API Layer -->
            <div class="layer api-layer">
                <div class="layer-number">3</div>
                <div class="layer-title">
                    <div class="layer-icon">🚪</div>
                    API Layer
                </div>
                
                <div class="components-grid">
                    <div class="component-card">
                        <div class="component-title">🔐 Authentication</div>
                        <div class="component-description">
                            Comprehensive authentication and authorization services for secure access control
                        </div>
                        <ul class="component-features">
                            <li>OAuth 2.0 / OpenID Connect</li>
                            <li>Multi-factor authentication (MFA)</li>
                            <li>Role-based access control (RBAC)</li>
                            <li>Single sign-on (SSO)</li>
                            <li>JWT token management</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Keycloak</span>
                            <span class="tech-badge">Auth0</span>
                            <span class="tech-badge">LDAP</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">⚡ Rate Limiting</div>
                        <div class="component-description">
                            Traffic management and rate limiting to ensure system stability and fair usage
                        </div>
                        <ul class="component-features">
                            <li>API quota management</li>
                            <li>Throttling and circuit breakers</li>
                            <li>Traffic shaping policies</li>
                            <li>DDoS protection</li>
                            <li>Usage analytics and monitoring</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Kong</span>
                            <span class="tech-badge">Envoy</span>
                            <span class="tech-badge">Istio</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">⚖️ Load Balancing</div>
                        <div class="component-description">
                            Intelligent traffic distribution and load balancing across multiple service instances
                        </div>
                        <ul class="component-features">
                            <li>Round-robin and weighted routing</li>
                            <li>Health check and failover</li>
                            <li>Geographic load distribution</li>
                            <li>Auto-scaling integration</li>
                            <li>Performance monitoring</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">NGINX</span>
                            <span class="tech-badge">HAProxy</span>
                            <span class="tech-badge">AWS ELB</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">📊 API Management</div>
                        <div class="component-description">
                            Comprehensive API lifecycle management, monitoring, and documentation
                        </div>
                        <ul class="component-features">
                            <li>API gateway management</li>
                            <li>Request/response transformation</li>
                            <li>API versioning and deprecation</li>
                            <li>Developer portal and documentation</li>
                            <li>Analytics and performance metrics</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">API Gateway</span>
                            <span class="tech-badge">Swagger/OpenAPI</span>
                            <span class="tech-badge">GraphQL</span>
                        </div>
                    </div>
                </div>
                
                <div class="layer-metrics">
                    <div class="metric">
                        <div class="metric-value">1M</div>
                        <div class="metric-label">API Calls/min</div>
                    </div>
                    <div class="metric">
                        <div class="metric-value">99.99%</div>
                        <div class="metric-label">API Availability</div>
                    </div>
                    <div class="metric">
                        <div class="metric-value">&lt;50ms</div>
                        <div class="metric-label">API Latency</div>
                    </div>
                </div>
            </div>
            
            <div class="data-flow-arrows">
                <div class="arrow">⬇</div>
            </div>
            
            <!-- Layer 4: Data Access Layer -->
            <div class="layer data-access-layer">
                <div class="layer-number">4</div>
                <div class="layer-title">
                    <div class="layer-icon">🔍</div>
                    Data Access Layer
                </div>
                
                <div class="components-grid">
                    <div class="component-card">
                        <div class="component-title">🏭 Factory Production Data</div>
                        <div class="component-description">
                            Specialized data access services for production-related information and metrics
                        </div>
                        <ul class="component-features">
                            <li>Production order data retrieval</li>
                            <li>Equipment performance metrics</li>
                            <li>Production schedule information</li>
                            <li>Quality control data access</li>
                            <li>Inventory and material tracking</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Spring Data</span>
                            <span class="tech-badge">JPA/Hibernate</span>
                            <span class="tech-badge">Redis Cache</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">👷 Workers Related Data</div>
                        <div class="component-description">
                            Human resources and workforce management data access services
                        </div>
                        <ul class="component-features">
                            <li>Employee profiles and skills</li>
                            <li>Shift scheduling and attendance</li>
                            <li>Training records and certifications</li>
                            <li>Performance tracking data</li>
                            <li>Safety incident reports</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">MongoDB Driver</span>
                            <span class="tech-badge">Elasticsearch</span>
                            <span class="tech-badge">GraphQL</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">🔧 Technicians Data Retrieval</div>
                        <div class="component-description">
                            Maintenance and technical staff data management and retrieval services
                        </div>
                        <ul class="component-features">
                            <li>Technician expertise and availability</li>
                            <li>Maintenance history and procedures</li>
                            <li>Equipment assignment tracking</li>
                            <li>Work order completion data</li>
                            <li>Parts inventory and procurement</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">REST APIs</span>
                            <span class="tech-badge">Connection Pooling</span>
                            <span class="tech-badge">Query Optimization</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">📊 Analytics Data Access</div>
                        <div class="component-description">
                            High-performance data access for analytics, reporting, and business intelligence
                        </div>
                        <ul class="component-features">
                            <li>Time-series data aggregation</li>
                            <li>Real-time analytics queries</li>
                            <li>Historical data retrieval</li>
                            <li>Cross-facility data correlation</li>
                            <li>ML model data preparation</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Apache Kafka</span>
                            <span class="tech-badge">Stream Processing</span>
                            <span class="tech-badge">Data Lakes</span>
                        </div>
                    </div>
                </div>
                
                <div class="layer-metrics">
                    <div class="metric">
                        <div class="metric-value">100K</div>
                        <div class="metric-label">Queries/sec</div>
                    </div>
                    <div class="metric">
                        <div class="metric-value">TB</div>
                        <div class="metric-label">Data Processed/day</div>
                    </div>
                    <div class="metric">
                        <div class="metric-value">&lt;10ms</div>
                        <div class="metric-label">Cache Hit Time</div>
                    </div>
                </div>
            </div>
            
            <div class="data-flow-arrows">
                <div class="arrow">⬇</div>
            </div>
            
            <!-- Layer 5: Database Layer -->
            <div class="layer database-layer">
                <div class="layer-number">5</div>
                <div class="layer-title">
                    <div class="layer-icon">💾</div>
                    Database Layer
                </div>
                
                <div class="components-grid">
                    <div class="component-card">
                        <div class="component-title">🍃 MongoDB</div>
                        <div class="component-description">
                            NoSQL document database for flexible, schema-less data storage and rapid development
                        </div>
                        <ul class="component-features">
                            <li>Employee profiles and HR data</li>
                            <li>Equipment configurations</li>
                            <li>Maintenance procedures and manuals</li>
                            <li>Quality inspection reports</li>
                            <li>Flexible document schemas</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Replica Sets</span>
                            <span class="tech-badge">Sharding</span>
                            <span class="tech-badge">Atlas</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">☁️ Amazon S3</div>
                        <div class="component-description">
                            Scalable object storage for large files, backups, and data lake implementation
                        </div>
                        <ul class="component-features">
                            <li>Raw IoT data archival</li>
                            <li>Document and media storage</li>
                            <li>Backup and disaster recovery</li>
                            <li>Data lake for analytics</li>
                            <li>Machine learning datasets</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">S3 Standard</span>
                            <span class="tech-badge">S3 Glacier</span>
                            <span class="tech-badge">S3 Analytics</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">❄️ Snowflake</div>
                        <div class="component-description">
                            Cloud data warehouse for analytics, business intelligence, and complex query processing
                        </div>
                        <ul class="component-features">
                            <li>Executive dashboards and KPIs</li>
                            <li>Financial reporting and analysis</li>
                            <li>Production analytics and trends</li>
                            <li>Cross-facility performance metrics</li>
                            <li>Advanced SQL analytics</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Auto-scaling</span>
                            <span class="tech-badge">Time Travel</span>
                            <span class="tech-badge">Data Sharing</span>
                        </div>
                    </div>
                    
                    <div class="component-card">
                        <div class="component-title">🔄 Data Integration</div>
                        <div class="component-description">
                            ETL/ELT processes and data synchronization between different database systems
                        </div>
                        <ul class="component-features">
                            <li>Real-time data synchronization</li>
                            <li>Batch ETL processing</li>
                            <li>Data quality and validation</li>
                            <li>Change data capture (CDC)</li>
                            <li>Data lineage and governance</li>
                        </ul>
                        <div class="tech-stack">
                            <span class="tech-badge">Apache Airflow</span>
                            <span class="tech-badge">Kafka Connect</span>
                            <span class="tech-badge">dbt</span>
                        </div>
                    </div>
                </div>
                
                <div class="layer-metrics">
                    <div class="metric">
                        <div class="metric-value">PB</div>
                        <div class="metric-label">Storage
