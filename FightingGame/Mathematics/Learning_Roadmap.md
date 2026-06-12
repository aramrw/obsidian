#math_roadmap

# Shader Mathematics Learning Roadmap

This roadmap is tailored for someone who has passed College Pre-Calculus I & II. It is ordered from foundational concepts (building on your existing knowledge) to the advanced mathematical techniques required for game physics and high-performance shader development.

## Phase 1: Foundations & Review (You've Got This)
*Leveraging your Pre-Calc background.*

1. **Trigonometry & Waves:**
    - [[Trigonometry]], [[Audio Processing]], [[Tan-Wave Shader]]
    - Review: Unit circle, sine/cosine waves, phase shifting.
2. **Vectors & Euclidean Geometry:**
    - [[Vectors]], [[Magnitude]], [[Normalization]], [[Dot Product]], [[Euclidean]]
    - Practice: Implement 2D vector length and dot product.
3. **Coordinate Systems:**
    - [[UV Normalization]], [[UV Mapping]], [[3D Geometry Formats]]

## Phase 2: Introduction to Linear Algebra
*Bridging from algebra to higher-dimensional space.*

1. **Matrices & Transformations:**
    - [[Matrices]], [[Affine Transformations]], [[Homogeneous Coordinates]]
    - Concept: Moving from equations to matrix multiplication.
2. **Spatial Logic:**
    - [[Distance Functions]], [[Collision Detection]], [[Minimum Bounding Box]], [[Planes]], [[Rays]]
3. **Determinants:**
    - [[Determinant]], [[Singular Matrix]]
    - Concept: Understanding why 0-determinant means information is lost.

## Phase 3: Intermediate Graphics & Signal Processing
*Moving into shader-specific math.*

1. **Filtering & Noise:**
    - [[Convolution]], [[Gaussian]], [[Perlin Noise]], [[Simplex Noise]]
2. **Domain Manipulation:**
    - [[Space Repetition]], [[Domain Warping]], [[Smoothstep Interpolation]], [[Lerp]]
3. **Advanced Geometry:**
    - [[Projection Matrix]], [[Cube Mesh]], [[Cubemap]], [[Skybox Shader]], [[Simple Raytracing]]

## Phase 4: Advanced Theoretical Math
*The "deep dive" for game engine architects.*

1. **Complex Analysis & Complex Numbers:**
    - [[Complex Numbers]], [[Analytic Continuation]], [[Riemann Hypothesis]]
2. **Advanced Linear Algebra:**
    - [[Eigenvalues and Eigenvectors]], [[LU Decomposition]], [[Numerical Linear Algebra]]
3. **Information Theory & Cryptography:**
    - [[Confusion]], [[Diffusion]], [[Hill Cypher]], [[Chaitin's Constant]], [[Graph Theory]]

---
*Recommended Workflow: "Learn-by-implementing." Start by writing small CLI utilities in Rust for every item in Phase 1 & 2 to solidify the mental model before moving into shader-writing in Phase 3.*
