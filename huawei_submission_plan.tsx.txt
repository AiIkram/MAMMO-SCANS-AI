import React, { useState } from 'react';
import { FileText, Upload, Activity, BarChart3, TrendingUp, Database, Users, CheckCircle, Clock, Brain, Zap, AlertCircle, Shield } from 'lucide-react';

const MammoScanAI = () => {
  const [activeView, setActiveView] = useState('dashboard');

  const stats = [
    { label: 'Total Scans Processed', value: '1,247', change: '+12%', icon: Database, color: 'blue' },
    { label: 'Avg. Dice Score', value: '0.72', sublabel: 'Multi-phase accuracy', icon: TrendingUp, color: 'emerald' },
    { label: 'Active Medical Centers', value: '4', sublabel: 'DUKE, NACT, ISPY1/2', icon: Users, color: 'purple' },
    { label: 'Avg. Processing Time', value: '1.8 min', sublabel: '95% time reduction', icon: Clock, color: 'amber' }
  ];

  const recentScans = [
    { id: 'DUKE_045_0002', status: 'Completed', dice: 0.94, time: '1.6 min', progress: 100 },
    { id: 'NACT_023_0001', status: 'Processing', dice: null, time: null, progress: 68 },
    { id: 'ISPY2_332_0002', status: 'Quality Check', dice: null, time: null, progress: 35 },
    { id: 'DUKE_128_0001', status: 'Completed', dice: 0.89, time: '2.1 min', progress: 100 }
  ];

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-50 via-blue-50 to-slate-100 p-8">
      <div className="max-w-7xl mx-auto">
        {/* Header */}
        <div className="mb-8">
          <div className="flex items-center justify-between mb-6">
            <div>
              <h1 className="text-4xl font-bold text-slate-900 mb-2">MAMMO-SCAN AI</h1>
              <p className="text-slate-600 text-lg">AI-Powered Breast Cancer Segmentation System</p>
            </div>
            <div className="flex items-center gap-3 bg-white px-6 py-3 rounded-xl shadow-md border border-slate-200">
              <div className="w-3 h-3 bg-emerald-500 rounded-full animate-pulse"></div>
              <span className="text-slate-700 font-medium">Huawei Cloud Active</span>
            </div>
          </div>

          {/* Navigation */}
          <div className="flex gap-3 bg-white p-2 rounded-xl shadow-md border border-slate-200">
            {['dashboard', 'upload', 'results', 'analytics'].map((view) => (
              <button
                key={view}
                onClick={() => setActiveView(view)}
                className={`flex-1 px-6 py-3 rounded-lg font-medium capitalize transition-all ${
                  activeView === view
                    ? 'bg-blue-600 text-white shadow-lg'
                    : 'text-slate-600 hover:bg-slate-100'
                }`}
              >
                {view}
              </button>
            ))}
          </div>
        </div>

        {/* Dashboard View */}
        {activeView === 'dashboard' && (
          <div className="space-y-6">
            {/* Stats Grid - 2 per row */}
            <div className="grid grid-cols-2 gap-6">
              {stats.map((stat, idx) => (
                <div key={idx} className="bg-white rounded-2xl p-6 shadow-lg border border-slate-200 hover:shadow-xl transition-all">
                  <div className="flex items-start justify-between mb-4">
                    <div>
                      <p className="text-slate-600 text-sm font-medium mb-1">{stat.label}</p>
                      <p className="text-4xl font-bold text-slate-900">{stat.value}</p>
                      {stat.sublabel && (
                        <p className="text-slate-500 text-sm mt-1">{stat.sublabel}</p>
                      )}
                      {stat.change && (
                        <p className="text-emerald-600 text-sm mt-1 font-medium">{stat.change} this month</p>
                      )}
                    </div>
                    <div className={`w-14 h-14 bg-${stat.color}-100 rounded-xl flex items-center justify-center`}>
                      <stat.icon className={`w-7 h-7 text-${stat.color}-600`} />
                    </div>
                  </div>
                </div>
              ))}
            </div>

            {/* Recent Scans */}
            <div className="bg-white rounded-2xl p-6 shadow-lg border border-slate-200">
              <div className="flex items-center justify-between mb-6">
                <h2 className="text-2xl font-bold text-slate-900">Recent Analysis Queue</h2>
                <div className="flex items-center gap-2 text-slate-600 text-sm">
                  <Activity className="w-4 h-4" />
                  <span>Live Processing</span>
                </div>
              </div>
              
              <div className="space-y-4">
                {recentScans.map((scan) => (
                  <div key={scan.id} className="bg-slate-50 rounded-xl p-5 border border-slate-200 hover:bg-slate-100 transition-all">
                    <div className="flex items-center justify-between mb-3">
                      <div className="flex-1">
                        <div className="flex items-center gap-3 mb-2">
                          <p className="font-mono text-lg font-semibold text-slate-900">{scan.id}</p>
                          <span className={`px-3 py-1 rounded-full text-xs font-medium ${
                            scan.status === 'Completed' 
                              ? 'bg-emerald-100 text-emerald-700 border border-emerald-200' 
                              : scan.status === 'Processing'
                              ? 'bg-blue-100 text-blue-700 border border-blue-200'
                              : 'bg-amber-100 text-amber-700 border border-amber-200'
                          }`}>
                            {scan.status}
                          </span>
                        </div>
                        {scan.dice && (
                          <div className="flex items-center gap-4 text-sm text-slate-600">
                            <span>Dice Score: <span className="text-emerald-600 font-semibold">{scan.dice}</span></span>
                            <span>Time: <span className="text-slate-900 font-medium">{scan.time}</span></span>
                          </div>
                        )}
                      </div>
                      <div className="flex items-center gap-4 ml-4">
                        <div className="w-48 bg-slate-200 rounded-full h-3 overflow-hidden">
                          <div
                            className={`h-full rounded-full transition-all duration-500 ${
                              scan.progress === 100 ? 'bg-emerald-500' : 'bg-blue-500'
                            }`}
                            style={{ width: `${scan.progress}%` }}
                          />
                        </div>
                        <span className="text-slate-900 font-semibold text-sm w-14 text-right">{scan.progress}%</span>
                      </div>
                    </div>
                  </div>
                ))}
              </div>
            </div>

            {/* System Status - 2 cards */}
            <div className="grid grid-cols-2 gap-6">
              <div className="bg-gradient-to-br from-emerald-50 to-teal-50 rounded-2xl p-6 shadow-lg border border-emerald-200">
                <div className="flex items-center gap-3 mb-4">
                  <CheckCircle className="w-6 h-6 text-emerald-600" />
                  <h3 className="text-xl font-bold text-slate-900">System Health</h3>
                </div>
                <div className="space-y-2">
                  <div className="flex justify-between text-sm">
                    <span className="text-slate-700">ModelArts API</span>
                    <span className="text-emerald-600 font-semibold">Online</span>
                  </div>
                  <div className="flex justify-between text-sm">
                    <span className="text-slate-700">Huawei Cloud ECS</span>
                    <span className="text-emerald-600 font-semibold">Active</span>
                  </div>
                  <div className="flex justify-between text-sm">
                    <span className="text-slate-700">GPU Inference</span>
                    <span className="text-emerald-600 font-semibold">Ready</span>
                  </div>
                  <div className="flex justify-between text-sm">
                    <span className="text-slate-700">Database Status</span>
                    <span className="text-emerald-600 font-semibold">Connected</span>
                  </div>
                </div>
              </div>

              <div className="bg-gradient-to-br from-blue-50 to-indigo-50 rounded-2xl p-6 shadow-lg border border-blue-200">
                <div className="flex items-center gap-3 mb-4">
                  <Brain className="w-6 h-6 text-blue-600" />
                  <h3 className="text-xl font-bold text-slate-900">AI Model Info</h3>
                </div>
                <div className="space-y-2 text-sm">
                  <div className="flex justify-between">
                    <span className="text-slate-700">Architecture</span>
                    <span className="text-slate-900 font-medium">nnU-Net 3D</span>
                  </div>
                  <div className="flex justify-between">
                    <span className="text-slate-700">Training Cases</span>
                    <span className="text-slate-900 font-medium">1,506 DCE-MRI</span>
                  </div>
                  <div className="flex justify-between">
                    <span className="text-slate-700">Validation Score</span>
                    <span className="text-blue-600 font-semibold">0.72 Dice</span>
                  </div>
                  <div className="flex justify-between">
                    <span className="text-slate-700">Model Version</span>
                    <span className="text-slate-900 font-medium">v2.1.0</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        )}

        {/* Upload View */}
        {activeView === 'upload' && (
          <div className="grid grid-cols-2 gap-6">
            <div className="bg-white rounded-2xl p-8 shadow-lg border border-slate-200">
              <h2 className="text-2xl font-bold text-slate-900 mb-6">Upload DCE-MRI Scan</h2>
              <div className="border-2 border-dashed border-blue-300 rounded-xl p-12 text-center hover:border-blue-500 hover:bg-blue-50 transition-all cursor-pointer">
                <Upload className="w-16 h-16 text-blue-600 mx-auto mb-4" />
                <p className="text-slate-900 text-lg font-medium mb-2">Drop NIfTI files here</p>
                <p className="text-slate-600 text-sm mb-4">or click to browse</p>
                <button className="px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium transition-all shadow-md">
                  Select Files
                </button>
              </div>

              <div className="mt-6 bg-slate-50 rounded-xl p-6 border border-slate-200">
                <h3 className="text-slate-900 font-semibold mb-4 flex items-center gap-2">
                  <Zap className="w-5 h-5 text-amber-500" />
                  Processing Pipeline
                </h3>
                <div className="space-y-3">
                  {[
                    'Quality Assessment',
                    'Multi-phase Integration (0000-0002)',
                    'nnU-Net Segmentation',
                    'Post-processing & Report'
                  ].map((step, idx) => (
                    <div key={idx} className="flex items-center gap-3 text-sm">
                      <div className="w-6 h-6 rounded-full bg-blue-100 border-2 border-blue-500 flex items-center justify-center">
                        <span className="text-blue-600 text-xs font-bold">{idx + 1}</span>
                      </div>
                      <span className="text-slate-700">{step}</span>
                    </div>
                  ))}
                </div>
              </div>
            </div>

            <div className="bg-white rounded-2xl p-8 shadow-lg border border-slate-200">
              <h2 className="text-2xl font-bold text-slate-900 mb-6">Supported Formats</h2>
              <div className="space-y-4">
                <div className="bg-gradient-to-r from-blue-50 to-cyan-50 rounded-xl p-6 border border-blue-200">
                  <h3 className="text-slate-900 font-semibold mb-2 flex items-center gap-2">
                    <FileText className="w-5 h-5 text-blue-600" />
                    NIfTI Format
                  </h3>
                  <p className="text-slate-700 text-sm">Primary format (.nii, .nii.gz)</p>
                  <p className="text-slate-600 text-xs mt-2">Recommended for DCE-MRI sequences</p>
                </div>

                <div className="bg-gradient-to-r from-purple-50 to-pink-50 rounded-xl p-6 border border-purple-200">
                  <h3 className="text-slate-900 font-semibold mb-2 flex items-center gap-2">
                    <FileText className="w-5 h-5 text-purple-600" />
                    DICOM Format
                  </h3>
                  <p className="text-slate-700 text-sm">Standard medical imaging (.dcm)</p>
                  <p className="text-slate-600 text-xs mt-2">Automatic conversion supported</p>
                </div>

                <div className="bg-slate-50 rounded-xl p-6 border border-slate-200">
                  <h3 className="text-slate-900 font-semibold mb-3">Requirements</h3>
                  <ul className="space-y-2 text-sm text-slate-700">
                    <li className="flex items-start gap-2">
                      <CheckCircle className="w-4 h-4 text-emerald-600 mt-0.5 flex-shrink-0" />
                      <span>Multi-phase DCE-MRI (phases 0000-0002 recommended)</span>
                    </li>
                    <li className="flex items-start gap-2">
                      <CheckCircle className="w-4 h-4 text-emerald-600 mt-0.5 flex-shrink-0" />
                      <span>Minimum resolution: 256x256 pixels</span>
                    </li>
                    <li className="flex items-start gap-2">
                      <CheckCircle className="w-4 h-4 text-emerald-600 mt-0.5 flex-shrink-0" />
                      <span>Maximum file size: 500MB per series</span>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        )}

        {/* Results View */}
        {activeView === 'results' && (
          <div className="grid grid-cols-2 gap-6">
            <div className="bg-white rounded-2xl p-8 shadow-lg border border-slate-200">
              <h2 className="text-2xl font-bold text-slate-900 mb-6">Segmentation Result</h2>
              <div className="bg-black rounded-xl overflow-hidden border-2 border-slate-300 mb-6">
                <img 
                  src="https://i.imgur.com/placeholder.jpg" 
                  alt="DUKE_045_0002_1 Segmentation"
                  className="w-full h-auto"
                  style={{ 
                    background: 'black',
                    minHeight: '400px',
                    objectFit: 'contain'
                  }}
                />
                <div className="bg-slate-100 p-3 border-t border-slate-300">
                  <p className="text-slate-900 font-mono text-sm font-semibold">DUKE_045_0002_1</p>
                </div>
              </div>
              
              <div className="grid grid-cols-2 gap-3">
                <div className="bg-gradient-to-br from-emerald-50 to-teal-50 rounded-lg p-4 border border-emerald-200">
                  <p className="text-slate-600 text-sm mb-1">Dice Score</p>
                  <p className="text-3xl font-bold text-slate-900">0.94</p>
                  <p className="text-emerald-600 text-xs mt-1 font-medium">Excellent</p>
                </div>
                <div className="bg-gradient-to-br from-blue-50 to-cyan-50 rounded-lg p-4 border border-blue-200">
                  <p className="text-slate-600 text-sm mb-1">Tumor Volume</p>
                  <p className="text-3xl font-bold text-slate-900">24.3 cm³</p>
                  <p className="text-blue-600 text-xs mt-1 font-medium">Measured</p>
                </div>
              </div>
            </div>

            <div className="bg-white rounded-2xl p-8 shadow-lg border border-slate-200">
              <h2 className="text-2xl font-bold text-slate-900 mb-6">Clinical Metrics</h2>
              
              <div className="space-y-4 mb-6">
                <div className="bg-slate-50 rounded-xl p-5 border border-slate-200">
                  <div className="flex justify-between items-center mb-2">
                    <span className="text-slate-600 text-sm font-medium">Processing Time</span>
                    <span className="text-slate-900 font-semibold">1.6 minutes</span>
                  </div>
                  <div className="w-full bg-slate-200 rounded-full h-2">
                    <div className="bg-emerald-500 h-2 rounded-full" style={{ width: '15%' }}></div>
                  </div>
                  <p className="text-xs text-slate-500 mt-1">Target: &lt;2 minutes</p>
                </div>

                <div className="bg-slate-50 rounded-xl p-5 border border-slate-200">
                  <div className="flex justify-between items-center mb-2">
                    <span className="text-slate-600 text-sm font-medium">Segmentation Quality</span>
                    <span className="text-emerald-600 font-semibold">Excellent</span>
                  </div>
                  <div className="w-full bg-slate-200 rounded-full h-2">
                    <div className="bg-emerald-500 h-2 rounded-full" style={{ width: '94%' }}></div>
                  </div>
                  <p className="text-xs text-slate-500 mt-1">94% accuracy</p>
                </div>

                <div className="bg-slate-50 rounded-xl p-5 border border-slate-200">
                  <div className="flex justify-between items-center mb-2">
                    <span className="text-slate-600 text-sm font-medium">Confidence Score</span>
                    <span className="text-slate-900 font-semibold">92%</span>
                  </div>
                  <div className="w-full bg-slate-200 rounded-full h-2">
                    <div className="bg-blue-500 h-2 rounded-full" style={{ width: '92%' }}></div>
                  </div>
                  <p className="text-xs text-slate-500 mt-1">High confidence</p>
                </div>
              </div>

              <div className="bg-gradient-to-br from-purple-50 to-pink-50 rounded-xl p-6 border border-purple-200 mb-6">
                <h3 className="text-slate-900 font-semibold mb-4 flex items-center gap-2">
                  <BarChart3 className="w-5 h-5 text-purple-600" />
                  Quantitative Analysis
                </h3>
                <div className="space-y-3 text-sm">
                  <div className="flex justify-between">
                    <span className="text-slate-700">Maximum Diameter</span>
                    <span className="text-slate-900 font-medium">3.8 cm</span>
                  </div>
                  <div className="flex justify-between">
                    <span className="text-slate-700">Surface Area</span>
                    <span className="text-slate-900 font-medium">18.6 cm²</span>
                  </div>
                  <div className="flex justify-between">
                    <span className="text-slate-700">Hausdorff Distance</span>
                    <span className="text-slate-900 font-medium">11.2 mm</span>
                  </div>
                  <div className="flex justify-between">
                    <span className="text-slate-700">Boundary Smoothness</span>
                    <span className="text-emerald-600 font-semibold">High</span>
                  </div>
                </div>
              </div>

              <button className="w-full px-6 py-4 bg-blue-600 hover:bg-blue-700 text-white rounded-xl font-medium transition-all shadow-md flex items-center justify-center gap-2">
                <FileText className="w-5 h-5" />
                Generate Clinical Report
              </button>
            </div>
          </div>
        )}

        {/* Analytics View */}
        {activeView === 'analytics' && (
          <div className="space-y-6">
            <div className="grid grid-cols-2 gap-6">
              <div className="bg-white rounded-2xl p-8 shadow-lg border border-slate-200">
                <h2 className="text-2xl font-bold text-slate-900 mb-6">Multi-Center Performance</h2>
                <div className="space-y-4">
                  {[
                    { center: 'DUKE', cases: 291, dice: 0.94, color: 'blue' },
                    { center: 'NACT', cases: 64, dice: 0.96, color: 'emerald' },
                    { center: 'ISPY1', cases: 171, dice: 0.76, color: 'amber' },
                    { center: 'ISPY2', cases: 980, dice: 0.90, color: 'purple' }
                  ].map((item) => (
                    <div key={item.center} className="bg-slate-50 rounded-xl p-5 border border-slate-200">
                      <div className="flex items-center justify-between mb-3">
                        <div>
                          <p className="text-slate-900 font-semibold text-lg">{item.center}</p>
                          <p className="text-slate-600 text-sm">{item.cases} cases</p>
                        </div>
                        <div className="text-right">
                          <p className="text-2xl font-bold text-slate-900">{item.dice}</p>
                          <p className="text-slate-600 text-xs">Dice Score</p>
                        </div>
                      </div>
                      <div className="w-full bg-slate-200 rounded-full h-2">
                        <div 
                          className={`bg-${item.color}-500 h-2 rounded-full transition-all`}
                          style={{ width: `${item.dice * 100}%` }}
                        ></div>
                      </div>
                    </div>
                  ))}
                </div>
              </div>

              <div className="bg-white rounded-2xl p-8 shadow-lg border border-slate-200">
                <h2 className="text-2xl font-bold text-slate-900 mb-6">Processing Statistics</h2>
                <div className="space-y-4">
                  <div className="bg-gradient-to-r from-blue-50 to-cyan-50 rounded-xl p-6 border border-blue-200">
                    <div className="flex items-center justify-between">
                      <div>
                        <p className="text-slate-600 text-sm mb-1 font-medium">Today's Scans</p>
                        <p className="text-4xl font-bold text-slate-900">48</p>
                      </div>
                      <Activity className="w-12 h-12 text-blue-600" />
                    </div>
                  </div>

                  <div className="bg-gradient-to-r from-emerald-50 to-teal-50 rounded-xl p-6 border border-emerald-200">
                    <div className="flex items-center justify-between">
                      <div>
                        <p className="text-slate-600 text-sm mb-1 font-medium">This Week</p>
                        <p className="text-4xl font-bold text-slate-900">287</p>
                      </div>
                      <TrendingUp className="w-12 h-12 text-emerald-600" />
                    </div>
                  </div>

                  <div className="bg-gradient-to-r from-purple-50 to-pink-50 rounded-xl p-6 border border-purple-200">
                    <div className="flex items-center justify-between">
                      <div>
                        <p className="text-slate-600 text-sm mb-1 font-medium">Total Processed</p>
                        <p className="text-4xl font-bold text-slate-900">1,247</p>
                      </div>
                      <Database className="w-12 h-12 text-purple-600" />
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <div className="bg-white rounded-2xl p-8 shadow-lg border border-slate-200">
              <h2 className="text-2xl font-bold text-slate-900 mb-6">System Performance Metrics</h2>
              <div className="grid grid-cols-3 gap-6">
                {[
                  { label: 'Average Processing Time', value: '1.8 min', target: '< 2 min', status: 'success' },
                  { label: 'System Uptime', value: '99.7%', target: '> 99%', status: 'success' },
                  { label: 'GPU Utilization', value: '78%', target: 'Optimal', status: 'success' }
                ].map((metric, idx) => (
                  <div key={idx} className="bg-slate-50 rounded-xl p-6 border border-slate-200">
                    <p className="text-slate-600 text-sm mb-2 font-medium">{metric.label}</p>
                    <p className="text-3xl font-bold text-slate-900 mb-1">{metric.value}</p>
                    <div className="flex items-center gap-2">
                      <CheckCircle className="w-4 h-4 text-emerald-600" />
                      <p className="text-emerald-600 text-xs font-medium">Target: {metric.target}</p>
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        )}
      </div>
    </div>
  );
};

export default MammoScanAI;