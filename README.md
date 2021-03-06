# vertexshader
#### Documentation file for mingl.cpp
#
#
# Passes tests 1-6
# Rasterize fill-in triangles/quads - Rasterizes wireframe of triangles/quads
# Color interpolation is done on the line segments and fill-in
# Z-buffering is done as well
# does not do geometric clipping, does viewport clipping in setPixels
#################################

// Vertex structure
// has X, Y, Z, W components
// and a color component
struct GLVertex

// Defines all of the matrix operation that can be performed
// The MGLOperations that involve matricies use this implementation
class MGLMatrix{

private:
	MGLfloat mMatrix[16];// Column major order
	
public:
	// Initialize to identity
	MGLMatrix()
	// Initialize all enties to zero then initialize diagonal to 1
	void SetIdentity()
	// Sets a matrix by deep copying into the object array from array
	void SetMatrix(const MGLfloat *newMatrix)
	// Sets a matrix by deep copying into the object array from the given matrix
	void SetMatrix(MGLMatrix newMatrix)
	// Crete new scalar matrix from given arguments
	// diagonal entry 1,2,3 are populated with x, y, z respectively
	// the matrix is right multiplied against the object matrix
	void ScaleMatrix(MGLfloat x, MGLfloat y, MGLfloat z){
	// uses the rotation matrix provided at
	// https://www.opengl.org/sdk/docs/man2/xhtml/glRotate.xml
	// matrix is right multiplied by object matrix
	void RotateMatrix(MGLfloat angle, MGLfloat X, MGLfloat Y,MGLfloat Z )
	// translate by x, y, z
	// matrix is right multiplied against object matrix
	void TranslateMatrix(MGLfloat x, MGLfloat y,MGLfloat z )
	// for each row in multiple, multiply by each column in object matrix
	MGLMatrix MultiplyMatrix(MGLMatrix multiple){
	// for each column in multiple, multiply by row in object matrix
   	 MGLMatrix MultiplyMatrixR(MGLMatrix multiple)
	// multiply the current object matrix by a vector/point
	GLVertex MultVertex(GLVertex vertex){
	//reference by []
	MGLfloat & operator[](int i)
	// left multiply given matrix
	MGLMatrix operator *(MGLMatrix matrix){
	// see the matrix	
	void seeMatrix()
	
};





// Read from the software framebuffer into data
// directly copies the framebuffer
// initializes buffers
// createas veiwport matrix
// calls renderTriangles
void mglReadPixels(MGLsize width,
                   MGLsize height,
                   MGLpixel *data)



// sets the polgon mode
// specifies that we have called glbegin
void mglBegin(MGLpoly_mode mode)

//The implicit edge function for three vertices
// used to see if pixel is in triangle
int orient2d(GLVertex a, GLVertex b, GLVertex c)

//Rasterize the triangle using a berry centric model
// perform depth interpolation as well as color interpolation
// uses orient2d for pixel condition.
void BerrycentricRasterization(GLVertex vertex0,
				GLVertex vertex1,
				GLVertex vertex2, 
				MGLpixel colors[3]){

// Renders the triangle using wireframe or filled in
// Transform cooridinates into screen space
// prepare to draw a line given two vertices, pass the 
// color constants and depth to the line drawing function
// or calls a berrycentric rasterizer
 void RenderTriangles(MGLMatrix screenMatrix, bool wireframe)


// Triangulates quadrilaterals
void RenderQuads(MGLMatrix screenMatrix, bool triangulate )


// Signifies the start of vertecies assignment
// Set the stack of the correct type to the current matrix
// call initial rasterization function for given polygon type
void mglEnd()


// dummy call to set_pixel(~~~~~~) with depth = 0
void set_pixel(MGLpixel color, float x, float y)


// Set the pixel specified by column x and row y
// to the given color argument 
// Z buffering is performed here
void set_pixel(MGLpixel color, float x, float y, float depth)


// dummy call to draw_line with depth1 = depth2 = 0	
void draw_line(MGLpixel pixelColor1,MGLpixel pixelColor2, int x0, int y0, int x1, int y1){


// Draw the line using a naive drawing algorithm
// Color interpolation is done using distance to each (x,y) pair to a point P on the line
// Interpolation is olny done on line if the colors are differnt between two vertices
// if they atre the same a single color is picked and used
// Interpolates the depth of a given pixel and passes the color, coordinate to draw and the depth 
// to the set_pixel function to store in the framebuffer
void draw_line(MGLpixel pixelColor1,MGLpixel pixelColor2, int x0, int y0, int x1, int y1, float depth1, float depth2)



//Dummy call to vertex3 with Z = 0
void mglVertex2(MGLfloat x,
                MGLfloat y) 


//Sets a vertex compnents of X,Y,Z to x, y, z respectively
// sets the color for that vertex
// Transforms vertex with modelview and projection matrices
// Push this onto a vector stack
void mglVertex3(MGLfloat x,
                MGLfloat y,
                MGLfloat z)


//Sets the current matrix mode 
// On a mode change it will save the current matrix type to its stack
// it will the set the current matrix to the top of the specified stack
void mglMatrixMode(MGLmatrix_mode mode)



//Save a copy of the current matrix to the stack and update its stack tracker
// Sets the new matrix to the old matrix (tracker - 1)
void mglPushMatrix()


//Decrement the stack tracker and set the current matrix to this matrix
void mglPopMatrix()


// Called using Matrix.SetIdentity()
void mglLoadIdentity()
 

// Called using Matrix.SetMatrix(matrix)
void mglLoadMatrix(const MGLfloat *matrix)


// Called using Matrix.MultiplyMatrix(matrix)
// This is a left multiplied matrix
void mglMultMatrix(const MGLfloat *matrix)

// Called using Matrix.Translate(x,y,z) for current matrix
void mglTranslate(MGLfloat x,
                  MGLfloat y,
                  MGLfloat z)


// Called using Matrix.RotateMatrix(angle,x,y,z) for current matrix
void mglRotate(MGLfloat angle,
               MGLfloat x,
               MGLfloat y,
               MGLfloat z)

// Called using Matrix.ScaleMatrix(x,y,z) for current matrix
void mglScale(MGLfloat x,
              MGLfloat y,
              MGLfloat z)


// Creates a frustrum that is right multiplied to the current matrix
//matrix is given by https://www.opengl.org/sdk/docs/man2/xhtml/glFrustum.xml
void mglFrustum(MGLfloat left,
                MGLfloat right,
                MGLfloat bottom,
                MGLfloat top,
                MGLfloat near,
                MGLfloat far)


// Creates an orthographic projection that is right multiplied against the current matrix
// Matrix is given by https://www.opengl.org/sdk/docs/man2/xhtml/glOrtho.xml
void mglOrtho(MGLfloat left,
              MGLfloat right,
              MGLfloat bottom,
              MGLfloat top,
              MGLfloat near,
              MGLfloat far)


// Set the current color for the drawn shapes using a global variable that is RGB
void mglColor(MGLbyte red,
              MGLbyte green,
              MGLbyte blue)
