IF   (DYNAMIC_OSGEARTH)
    ADD_DEFINITIONS(-DOSGEARTHFEATURES_LIBRARY)
ELSE (DYNAMIC_OSGEARTH)
    ADD_DEFINITIONS(-DOSGEARTHFEATURES_LIBRARY_STATIC)
ENDIF(DYNAMIC_OSGEARTH)

IF (GEOS_FOUND)
    ADD_DEFINITIONS(-DOSGEARTH_HAVE_GEOS)
ENDIF(GEOS_FOUND)

SET(LIB_NAME osgEarthFeatures)

SET(HEADER_PATH ${OSGEARTH_SOURCE_DIR}/include/${LIB_NAME})
SET(LIB_PUBLIC_HEADERS
    AltitudeFilter
    BufferFilter
    BuildGeometryFilter  
    BuildTextFilter
    BuildTextOperator
    CentroidFilter
    Common
    ConvertTypeFilter
    CropFilter
    ExtrudeGeometryFilter    
    Feature
    FeatureCursor
    FeatureDisplayLayout
    FeatureDrawSet
    FeatureIndex
    FeatureListSource
    FeatureModelGraph
    FeatureModelSource
    FeatureSource
    FeatureSourceIndexNode
    FeatureTileSource
    Filter
    FilterContext
    GeometryCompiler
    GeometryUtils
    LabelSource
    MeshClamper
    OgrUtils
    OptimizerHints
    PolygonizeLines
    ResampleFilter
    ScaleFilter
    Session
    ScatterFilter
    Script
    ScriptEngine
    SubstituteModelFilter
    TessellateOperator
    TextSymbolizer
    TransformFilter
    VirtualFeatureSource
)

set(LIB_COMMON_FILES
    AltitudeFilter.cpp
    BufferFilter.cpp
    BuildGeometryFilter.cpp 
    BuildTextFilter.cpp
    BuildTextOperator.cpp
    CentroidFilter.cpp
    ConvertTypeFilter.cpp
    CropFilter.cpp
    ExtrudeGeometryFilter.cpp    
    Feature.cpp
    FeatureCursor.cpp
    FeatureDisplayLayout.cpp
    FeatureDrawSet.cpp
	FeatureListSource.cpp
    FeatureModelGraph.cpp
    FeatureModelSource.cpp
    FeatureSource.cpp
    FeatureSourceIndexNode.cpp
    FeatureTileSource.cpp
    Filter.cpp
    FilterContext.cpp
    GeometryCompiler.cpp
	GeometryUtils.cpp
    LabelSource.cpp
    MeshClamper.cpp
    OgrUtils.cpp
    OptimizerHints.cpp
    PolygonizeLines.cpp
    ResampleFilter.cpp
    ScaleFilter.cpp
    Session.cpp
    ScatterFilter.cpp
    ScriptEngine.cpp
    SubstituteModelFilter.cpp
    TessellateOperator.cpp
    TextSymbolizer.cpp
    TransformFilter.cpp
    VirtualFeatureSource.cpp
)

ADD_LIBRARY(${LIB_NAME} ${OSGEARTH_USER_DEFINED_DYNAMIC_OR_STATIC}
    ${LIB_PUBLIC_HEADERS}
    ${LIB_COMMON_FILES}
)

INCLUDE_DIRECTORIES(${GDAL_INCLUDE_DIR} )


IF (WIN32)
  LINK_EXTERNAL(${LIB_NAME} ${TARGET_EXTERNAL_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} ${MATH_LIBRARY})
ELSE(WIN32)
  LINK_EXTERNAL(${LIB_NAME} ${TARGET_EXTERNAL_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} ${MATH_LIBRARY})
ENDIF(WIN32)

LINK_INTERNAL(${LIB_NAME}
	osgEarth
	osgEarthSymbology
)

LINK_WITH_VARIABLES(${LIB_NAME} OSG_LIBRARY OSGUTIL_LIBRARY OSGSIM_LIBRARY OSGTERRAIN_LIBRARY OSGDB_LIBRARY OSGFX_LIBRARY OSGVIEWER_LIBRARY OSGTEXT_LIBRARY OSGGA_LIBRARY OPENTHREADS_LIBRARY)


IF(ANDROID)
	SETUP_LIBRARY(${LIB_NAME})
ELSE()
	LINK_CORELIB_DEFAULT(${LIB_NAME} ${CMAKE_THREAD_LIBS_INIT} ${MATH_LIBRARY})

	INCLUDE(ModuleInstall OPTIONAL)
ENDIF()
