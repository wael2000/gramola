ARG FROM_IMAGE
FROM ${FROM_IMAGE} AS BASE

ENV ARGOCD_VERSION=v2.1.2
ENV OC_VERSION=4.8.13

RUN microdnf install --nodocs -y git openssh-clients tar gzip  && \
    microdnf clean all

RUN curl -o /tmp/argocd -L https://github.com/argoproj/argo-cd/releases/download/${ARGOCD_VERSION}/argocd-linux-amd64 && cd /usr/bin && cp /tmp/argocd . && chmod a+x /usr/bin/argocd && rm -f /tmp/argocd
RUN curl -o /tmp/oc.tar.gz -L https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/${OC_VERSION}/openshift-client-linux-${OC_VERSION}.tar.gz && cd /usr/bin && tar -xvzf /tmp/oc.tar.gz && chmod a+x /usr/bin/oc && chmod a+x /usr/bin/kubectl && rm -f /tmp/oc.tar.gz


# COPY --from=builder /tmp/openshift-pipelines-git-init ${KO_APP}/${BINARY}
# COPY openshift/ci-operator/uidwrapper ${KO_APP}/git-init
# COPY --from=builder /opt/app-root/src/go/src/github.com/tektoncd/pipeline/cmd/git-init/kodata/ ${KO_DATA_PATH}/

# RUN chgrp -R 0 ${KO_APP} && \
#     chmod -R g=u ${KO_APP} /etc/passwd

# LABEL \
#       com.redhat.component="openshift-pipelines-git-init-rhel8-container" \
#       name="openshift-pipelines-tech-preview/pipelines-git-init-rhel8" \
#       version="v1.3.1" \
#       summary="Red Hat OpenShift Pipelines Git-init" \
#       maintainer="pradkuma@redhat.com" \
#       description="Red Hat OpenShift Pipelines Git-init" \
#       io.k8s.display-name="Red Hat OpenShift Pipelines Git-init"