
#  NoteBook Contents:

- Kmean clustering for `docword.kos.txt` dataset
- Kmean clustering for `docword.nips.txt` dataset
- Kmean clustering for `docword.enron.txt` dataset

# Kmean Algorithm

We are using `Jaccard distance` for comparing documents.

$$Jaccard\ Distance = \frac{\# (a \cap b)}{\# (a \cup b)}$$

parameters for Kmean:

- k (default = 3) = Number of centroids
- threshold (default = 0.1) = To stop updating centroids
- random_state (default = 42) = determines how we initialize centroids at the start of algorithm.

The Kmeans class contains the following functions:

1. **initialize_centroids**:
   - Parameters for this are **init** we can assign this parameter to 'kmean' or 'kmean++' depending on wheather we like to implement k-means or k-means ++ algorithm. By default it is kmean.
   - In kmean we randomly assign centroids at the start of the algorithm, whereas in kmean++ we try to initialise centroids as far apart as possible. In order to do this our function assigns probabilities to all the instances in the dataset (except for those instances that are centroids themselves) in such a way that the points that are furhter from all the centroids gets assigned high probability compared to the points that are closer.
   - Take a new centroid $ c(i)$, choosing an instance $x(i)$ with probability:$$\frac{D(X(i))^2}{\sum_{j=1}^{m}D(X(j))^2}$$ where$ m$ is the number of instances and  $D(x(i))$ is the distance between the instance $x(i)$ and the closest centroid that was already chosen.This is how the kmean++ assigns probailities to the instances.

2. **update_centroids**:
    - This is used to recompute centroids after we update our clusters.
    - **The centroid within a cluster is determined by selecting the instance that minimizes the sum of distances (measured using Jaccard distance) from that instance to all other instances within the same cluster.**

3. **stopping_criterion**:
    - The Kmeans algorithm should stop after the certroids start to converge.
    - To ensure convergence, we establish a specific threshold. If the average distance between the old centroids and the new centroids falls below this threshold, we conclude the algorithm. This practice helps in determining when the algorithm has effectively reached a stable state and further iterations are unnecessary.

4. **fit**:
    - The function parameters consist of a numpy array called distances, sized $n \times n$ where $n$ signifies the number of documents, containing information on the distance from one document to every other document. Another parameter, **max_iterations**, determines the maximum number of iterations allowed for updating centroids, with a default value of 10. Additionally, the **init** parameter specifies the initialization method, which can be either 'kmean' or 'kmean++', with 'kmean' set as the default option.
    - Initially, centroids are initialized by invoking the **initialize_centroid** function.
    - Subsequently, an iteration process begins, where centroids are updated in each iteration by calling the **update_centroid** function. 
    - To determine if the termination criterion is satisfied, indicating the convergence of centroids, the **stopping_criterion** function is invoked.
    
5. WCSS:
    - To obtain the optimal value of k, it's essential to employ a performance metric that facilitates comparison among clustering results obtained for various values of k.
    - WCSS computes the sums of squares of the distances from the centroid to each instance within the cluster.This works as a performance metric.
    - If WCSS is large then the points are scattered in the cluster.If it's less then the instances are close to each other(means they are more similar to each other).

For KOS Dataset the results are the following.
- Optimal value of k is 9.
- Time taken is 6.08 sec.
- memory taken is 12.0 MB.

For NIPS Dataset the results are the following.
- Optimal Value of k is 11.
- Time taken is 0.43 sec
- Memory is 4 MB

For ENRON Dataset the results are the following.
- Optimal Value of k is 15.
- Time taken is 2.05 sec.
- Memory is 16 MB.

    
